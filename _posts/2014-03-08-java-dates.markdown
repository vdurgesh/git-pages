---
layout: post
title:  "Timezone"
date:   2014-03-08 10:03:00
categories: java
---

I spend last two week, trying to solve one common problem with java dates on one of web application. It was a simple requirement that User should able to enter date and time on their specified time zone and able to see same time on various reports. 

It is a global web application with various departments on various countries, so system has to mange departments and their specific time zone (based on location) and every user of individual department should enter and see dates on same time zone.

Simple, Isn’t it? Not really, it is not so simple with java calendar and MySQL database located on different time zone. You have to be very specific and need to consider following important points.

If your application needs to store dates and time internally, for instance in a database, convert it to UTC time before storing it. It is a lot easier to manage and look for a given date and time, when all dates and times are stored in UTC. If the dates and times were stored in different time zones in a database, it would be hard to look for all dates before or after a certain date. You would need to convert the dates and time zones while searching, in order to compare to the date of the search criteria. This doesn't really work.

When a user types in a date and time, they usually do so in their own time zone. If a user in another time zone needs to look at that date and time, that user would often like to see that date and time converted to his own time zone.

In pretty simple way, we can follow java calendar logic for converting timezone,
1. Create a GregorianCalendar instance.
2. Set the time zone to UTC. 
3. Set the time (in mills or hour, min, sec). 
4. Change the time zone to the desired target time zone.

{% highlight ruby %}
Calendar calendar = new GregorianCalendar();  
calendar.setTimeZone(TimeZone.getTimeZone("UTC"));  
calendar.set(Calendar.HOUR_OF_DAY, 25);  
System.out.println("UTC: " + calendar.get(Calendar.HOUR_OF_DAY)); 
System.out.println("UTC: " + calendar.getTimeInMillis());  
calendar.setTimeZone(TimeZone.getTimeZone("Europe/Copenhagen")); 
System.out.println("CPH: " + calendar.get(Calendar.HOUR_OF_DAY)); 
System.out.println("CPH: " + calendar.getTimeInMillis());  
calendar.setTimeZone(TimeZone.getTimeZone("America/New_York")); 
System.out.println("NYC: " + calendar.get(Calendar.HOUR_OF_DAY));
System.out.println("NYC: " + calendar.getTimeInMillis());

{% endhighlight %}


You might need to consider little more overhead with Spring MVC with Thymeleaf and joda time api and MySQL J2EE application, I did following to achieve expected behavior on my web application.

1. On Spring MVC, wrote and plugged in DateTimeEditor, which extends PropertyEditorSupport


{% highlight ruby %}
package controller.util;

import java.beans.PropertyEditorSupport;

import org.joda.time.DateTime;
import org.joda.time.DateTimeZone;
import org.joda.time.format.DateTimeFormat;
import org.joda.time.format.DateTimeFormatter;
import org.springframework.util.StringUtils;

/**
 * Custom PropertyEditorSupport to convert from String to
 * Date using JODA.
 */
public class DateTimeEditor extends PropertyEditorSupport {

    private final DateTimeFormatter formatter;
    private final boolean allowEmpty;

    /**
     * Create a new DateTimeEditor instance, using the given format for
     * parsing and rendering.
     * <p/>
     * The "allowEmpty" parameter states if an empty String should be allowed
     * for parsing, i.e. get interpreted as null value. Otherwise, an
     * IllegalArgumentException gets thrown.
     *
     * @param dateFormat DateFormat to use for parsing and rendering
     * @param allowEmpty if empty strings should be allowed
     */
    public DateTimeEditor( String dateFormat, boolean allowEmpty ) {
        this.formatter = DateTimeFormat.forPattern( dateFormat );
        this.allowEmpty = allowEmpty;
    }

// ------------------------ OVERRIDING METHODS ------------------------

    /**
     * Format the YearMonthDay as String, using the specified format.
     *
     * @return DateTime formatted string
     */
    public String getAsText() {
    		if(getValue() == null) {
    			return ""; //return null if the property is null
    		}
    		DateTime value = (( DateTime ) getValue()).withZone(DateTimeZone.UTC); 
    		//if the property is not null, read it as a DateTime
    		return value != null ? value.toString() : "";
    }

    /**
     * Parse the value from the given text, using the specified format.
     *
     * @param text
     * @throws IllegalArgumentException
     */
    public void setAsText( String text ) throws IllegalArgumentException {
    		if ( allowEmpty && !StringUtils.hasText( text ) ) {
			// Treat empty String as null value.
			setValue( null );
		} else {
			DateTime val = formatter.parseDateTime( text ).withZoneRetainFields(DateTimeZone.UTC); 
			setValue( val );
		}
    }
}

{% endhighlight %}


Other Mapper Util for Actual TimeZone conversion.


{% highlight ruby %}
package utils;


import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.TimeZone;

import org.joda.time.DateTime;
import org.joda.time.DateTimeZone;
import org.joda.time.format.DateTimeFormat;
import org.joda.time.format.DateTimeFormatter;

public class DefaultCalendar {

   
    /* Intialized Default TimeZone for JVM */

    static  {
        TimeZone.getTimeZone("UTC");
        DateTimeZone.setDefault(DateTimeZone.UTC);
    }
    
    /* Convert DateTime to String for report purpose */
    public static String formatTime(DateTime date) {
    		DateTimeFormatter parser = DateTimeFormat.forPattern(DATE_TIME_FORMAT);
    		return parser.withZone(USER_TZ).print(date);
    }
    
    /* Convert Database UTC dates to User TimeZone */
    public static Calendar toUserTimeZone(DateTime date) {
		return date.withZone(DateTimeZone.forID(USER_TIMEZONE)).toGregorianCalendar(); 
    }
    
    /*Convert User timezone to System/Database Timezone*/
    public static DateTime toSystemTimeZone(Calendar date) {
    		return new DateTime(date).withZone(DateTimeZone.UTC);
    }

}

{% endhighlight %}


And finally ran following commands for MySQL database.

{% highlight ruby %}

--Session and global Time to UTC
SET time_zone = '+00:00';
SET GLOBAL time_zone = '+00:00';
{% endhighlight %}


To verify what timezone your MySQL session is using, just execute this:

{% highlight ruby %}

SELECT @@global.time_zone, @@session.time_zone;

{% endhighlight %}
