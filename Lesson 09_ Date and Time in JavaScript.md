### **Lesson 9: Date and Time in JavaScript**

Date and time handling is crucial for applications dealing with scheduling, logging, user interfaces, and data processing. JavaScript provides the `Date` object for date and time manipulation, along with modern APIs like `Intl.DateTimeFormat` for internationalization. This comprehensive lesson covers everything about dates and times in JavaScript with extensive examples and best practices.

#### **1. What are Dates and Times in JavaScript?**

- **Definition:** JavaScript uses the `Date` object to represent dates and times as milliseconds since January 1, 1970, 00:00:00 UTC (Unix epoch).
- **Why Needed:** Essential for timestamps, scheduling, calendars, logging, and time-based operations.
- **Characteristics:** Mutable, represents both date and time, timezone-aware.

**Example:** User registration dates, event scheduling, log timestamps, countdown timers.

#### **2. Creating Date Objects**

##### **2.1 Current Date and Time**

```javascript
/**
 * new Date() - Creates a Date object with current date and time
 * @returns {Date} New Date object representing current moment
 */
const now = new Date();
console.log(now); // Current date and time

/**
 * Date.now() - Returns current timestamp in milliseconds
 * @returns {number} Milliseconds since Unix epoch
 */
const timestamp = Date.now();
console.log(timestamp); // e.g., 1699123456789
```

##### **2.2 Creating Specific Dates**

```javascript
/**
 * new Date(year, month, day, hours, minutes, seconds, milliseconds)
 * Note: Month is 0-indexed (0 = January, 11 = December)
 * @param {number} year - Full year (e.g., 2023)
 * @param {number} month - Month (0-11)
 * @param {number} [day=1] - Day of month (1-31)
 * @param {number} [hours=0] - Hours (0-23)
 * @param {number} [minutes=0] - Minutes (0-59)
 * @param {number} [seconds=0] - Seconds (0-59)
 * @param {number} [milliseconds=0] - Milliseconds (0-999)
 * @returns {Date} Date object for specified date/time
 */

// Specific date
const birthday = new Date(1990, 5, 15); // June 15, 1990
const meeting = new Date(2023, 11, 25, 14, 30); // Dec 25, 2023, 2:30 PM

// From timestamp
const fromTimestamp = new Date(1699123456789);

// From ISO string
const fromISO = new Date('2023-10-04T12:30:45.123Z');

// From date string (avoid using - browser dependent)
const fromString = new Date('October 4, 2023 12:30:45');

// Common date string patterns from user code
let myCreatedDate = new Date("07-10-2025");
console.log(myCreatedDate.toDateString());
console.log(myCreatedDate.toTimeString());
console.log(myCreatedDate.toLocaleString());
console.log(myCreatedDate.getTimezoneOffset()); // Minutes difference from UTC
console.log(typeof myCreatedDate); // "object"
```

##### **2.3 Parsing Date Strings**

```javascript
/**
 * Date.parse(dateString) - Parses date string and returns timestamp
 * @param {string} dateString - Date string to parse
 * @returns {number} Timestamp in milliseconds, or NaN if invalid
 */

// ISO 8601 format (recommended)
Date.parse('2023-10-04T12:30:45.123Z'); // 1696422645123
Date.parse('2023-10-04T12:30:45'); // Local timezone
Date.parse('2023-10-04'); // Midnight local time

// RFC 2822 format
Date.parse('Wed, 04 Oct 2023 12:30:45 GMT');

// US format (avoid - ambiguous)
Date.parse('10/04/2023'); // October 4 or April 10?

// Safe parsing function
function safeParseDate(dateString) {
  const timestamp = Date.parse(dateString);
  if (isNaN(timestamp)) {
    throw new Error(`Invalid date string: ${dateString}`);
  }
  return new Date(timestamp);
}
```

#### **3. Date Methods - Getters**

##### **3.1 Getting Date Components**

```javascript
const date = new Date('2023-10-04T14:30:45.123Z');

/**
 * Date.prototype.getFullYear() - Get full year (4 digits)
 * @returns {number} Year (e.g., 2023)
 */
date.getFullYear(); // 2023

/**
 * Date.prototype.getMonth() - Get month (0-11)
 * @returns {number} Month (0 = January, 11 = December)
 */
date.getMonth(); // 9 (October)

/**
 * Date.prototype.getDate() - Get day of month (1-31)
 * @returns {number} Day of month
 */
date.getDate(); // 4

/**
 * Date.prototype.getDay() - Get day of week (0-6)
 * @returns {number} Day of week (0 = Sunday, 6 = Saturday)
 */
date.getDay(); // 3 (Wednesday)

// Common date component access patterns
let newDate = new Date();
console.log(newDate.getMonth() + 1); // Month (1-12, adding 1 because getMonth() is 0-indexed)
console.log(newDate.getDate()); // Day of month (1-31)
console.log(newDate.getDay()); // Day of week (0-6, 0 = Sunday)
console.log(newDate.getFullYear()); // Full year (4 digits)
```

##### **3.2 Getting Time Components**

```javascript
const time = new Date('2023-10-04T14:30:45.123Z');

/**
 * Date.prototype.getHours() - Get hours (0-23)
 * @returns {number} Hours in 24-hour format
 */
time.getHours(); // 14

/**
 * Date.prototype.getMinutes() - Get minutes (0-59)
 * @returns {number} Minutes
 */
time.getMinutes(); // 30

/**
 * Date.prototype.getSeconds() - Get seconds (0-59)
 * @returns {number} Seconds
 */
time.getSeconds(); // 45

/**
 * Date.prototype.getMilliseconds() - Get milliseconds (0-999)
 * @returns {number} Milliseconds
 */
time.getMilliseconds(); // 123
```

##### **3.3 UTC vs Local Time Methods**

```javascript
const date = new Date('2023-10-04T14:30:45.123Z');

// Local time methods
date.getFullYear();   // Local year
date.getMonth();      // Local month
date.getDate();       // Local day
date.getHours();      // Local hours

// UTC methods
date.getUTCFullYear(); // UTC year
date.getUTCMonth();    // UTC month
date.getUTCDate();     // UTC day
date.getUTCHours();    // UTC hours

// Timezone offset
date.getTimezoneOffset(); // Minutes difference from UTC
```

##### **3.4 Getting Timestamps**

```javascript
const date = new Date();

/**
 * Date.prototype.getTime() - Get timestamp in milliseconds
 * @returns {number} Milliseconds since Unix epoch
 */
date.getTime(); // e.g., 1699123456789

/**
 * Date.prototype.valueOf() - Same as getTime()
 * @returns {number} Milliseconds since Unix epoch
 */
date.valueOf(); // Same as getTime()

// Static methods
Date.now(); // Current timestamp
Date.parse('2023-10-04T12:00:00Z'); // Parse to timestamp

// Timestamp conversions
let myTimeStamp = Date.now();
console.log(myTimeStamp); // Current timestamp in milliseconds
console.log(myCreatedDate.getTime()); // Timestamp from date object
console.log(Math.floor(Date.now() / 1000)); // Convert to seconds
```

#### **4. Date Methods - Setters**

##### **4.1 Setting Date Components**

```javascript
const date = new Date();

/**
 * Date.prototype.setFullYear(year, month, day) - Set full year
 * @param {number} year - Year to set
 * @param {number} [month] - Month to set (0-11)
 * @param {number} [day] - Day to set (1-31)
 * @returns {number} New timestamp
 */
date.setFullYear(2024); // Set to 2024
date.setFullYear(2024, 5, 15); // Set to June 15, 2024

/**
 * Date.prototype.setMonth(month, day) - Set month
 * @param {number} month - Month to set (0-11)
 * @param {number} [day] - Day to set (1-31)
 * @returns {number} New timestamp
 */
date.setMonth(11); // Set to December
date.setMonth(11, 25); // Set to December 25

/**
 * Date.prototype.setDate(day) - Set day of month
 * @param {number} day - Day to set (1-31)
 * @returns {number} New timestamp
 */
date.setDate(15); // Set to 15th of current month
```

##### **4.2 Setting Time Components**

```javascript
const time = new Date();

/**
 * Date.prototype.setHours(hours, minutes, seconds, milliseconds) - Set hours
 * @param {number} hours - Hours to set (0-23)
 * @param {number} [minutes] - Minutes to set (0-59)
 * @param {number} [seconds] - Seconds to set (0-59)
 * @param {number} [milliseconds] - Milliseconds to set (0-999)
 * @returns {number} New timestamp
 */
time.setHours(14); // Set to 2 PM
time.setHours(14, 30, 45, 123); // Set to 2:30:45.123 PM

/**
 * Date.prototype.setMinutes(minutes, seconds, milliseconds) - Set minutes
 * @param {number} minutes - Minutes to set (0-59)
 * @param {number} [seconds] - Seconds to set (0-59)
 * @param {number} [milliseconds] - Milliseconds to set (0-999)
 * @returns {number} New timestamp
 */
time.setMinutes(45); // Set minutes to 45

/**
 * Date.prototype.setSeconds(seconds, milliseconds) - Set seconds
 * @param {number} seconds - Seconds to set (0-59)
 * @param {number} [milliseconds] - Milliseconds to set (0-999)
 * @returns {number} New timestamp
 */
time.setSeconds(30); // Set seconds to 30

/**
 * Date.prototype.setMilliseconds(milliseconds) - Set milliseconds
 * @param {number} milliseconds - Milliseconds to set (0-999)
 * @returns {number} New timestamp
 */
time.setMilliseconds(500); // Set to 500ms
```

##### **4.3 UTC Setters**

```javascript
const date = new Date();

// UTC setters (similar to local setters)
date.setUTCFullYear(2024);
date.setUTCMonth(11);
date.setUTCDate(25);
date.setUTCHours(14);
date.setUTCMinutes(30);
date.setUTCSeconds(45);
date.setUTCMilliseconds(123);
```

#### **5. Date Formatting and Display**

##### **5.1 Built-in Formatting Methods**

```javascript
const date = new Date('2023-10-04T14:30:45.123Z');

/**
 * Date.prototype.toString() - Convert to readable string
 * @returns {string} Date as string in local timezone
 */
date.toString(); // "Wed Oct 04 2023 14:30:45 GMT+0000 (Coordinated Universal Time)"

/**
 * Date.prototype.toDateString() - Date part only
 * @returns {string} Date part as string
 */
date.toDateString(); // "Wed Oct 04 2023"

/**
 * Date.prototype.toTimeString() - Time part only
 * @returns {string} Time part as string
 */
date.toTimeString(); // "14:30:45 GMT+0000 (Coordinated Universal Time)"

/**
 * Date.prototype.toISOString() - ISO 8601 format (recommended)
 * @returns {string} Date in ISO 8601 format
 */
date.toISOString(); // "2023-10-04T14:30:45.123Z"

/**
 * Date.prototype.toUTCString() - UTC format
 * @returns {string} Date in UTC format
 */
date.toUTCString(); // "Wed, 04 Oct 2023 14:30:45 GMT"

/**
 * Date.prototype.toLocaleString() - Localized format
 * @param {string|string[]} [locales] - BCP 47 language tags
 * @param {object} [options] - Formatting options
 * @returns {string} Localized date string
 */
date.toLocaleString('en-US'); // "10/4/2023, 2:30:45 PM"
date.toLocaleString('de-DE'); // "4.10.2023, 14:30:45"
date.toLocaleString('ja-JP'); // "2023/10/4 14:30:45"
```

##### **5.2 Custom Date Formatting**

```javascript
/**
 * Format date to custom string
 * @param {Date} date - Date to format
 * @param {string} format - Format string
 * @returns {string} Formatted date string
 */
function formatDate(date, format = 'YYYY-MM-DD') {
  const year = date.getFullYear();
  const month = String(date.getMonth() + 1).padStart(2, '0');
  const day = String(date.getDate()).padStart(2, '0');
  const hours = String(date.getHours()).padStart(2, '0');
  const minutes = String(date.getMinutes()).padStart(2, '0');
  const seconds = String(date.getSeconds()).padStart(2, '0');

  return format
    .replace('YYYY', year)
    .replace('MM', month)
    .replace('DD', day)
    .replace('HH', hours)
    .replace('mm', minutes)
    .replace('ss', seconds);
}

const date = new Date('2023-10-04T14:30:45');
formatDate(date, 'YYYY-MM-DD'); // "2023-10-04"
formatDate(date, 'DD/MM/YYYY HH:mm:ss'); // "04/10/2023 14:30:45"
```

##### **5.3 Intl.DateTimeFormat (Modern Approach)**

```javascript
/**
 * Intl.DateTimeFormat - Modern internationalization API
 * @param {string|string[]} locales - BCP 47 language tags
 * @param {object} options - Formatting options
 */

// Basic usage
const formatter = new Intl.DateTimeFormat('en-US');
formatter.format(new Date()); // "10/4/2023"

// With options
const detailedFormatter = new Intl.DateTimeFormat('en-US', {
  year: 'numeric',
  month: 'long',
  day: 'numeric',
  hour: '2-digit',
  minute: '2-digit',
  second: '2-digit',
  timeZone: 'America/New_York'
});

detailedFormatter.format(new Date()); // "October 4, 2023, 10:30:45 AM"

// Multiple locales
const multiFormatter = new Intl.DateTimeFormat(['en-US', 'de-DE'], {
  dateStyle: 'full',
  timeStyle: 'short'
});

multiFormatter.format(new Date());
// "Wednesday, October 4, 2023 at 10:30 AM" (English)
// "Mittwoch, 4. Oktober 2023 um 10:30" (German)
```

#### **6. Date Arithmetic and Manipulation**

##### **6.1 Adding/Subtracting Time**

```javascript
const date = new Date('2023-10-04T12:00:00');

/**
 * Add days to date
 * @param {Date} date - Base date
 * @param {number} days - Days to add
 * @returns {Date} New date with days added
 */
function addDays(date, days) {
  const result = new Date(date);
  result.setDate(result.getDate() + days);
  return result;
}

addDays(date, 7); // 7 days later
addDays(date, -3); // 3 days earlier

/**
 * Add hours to date
 * @param {Date} date - Base date
 * @param {number} hours - Hours to add
 * @returns {Date} New date with hours added
 */
function addHours(date, hours) {
  const result = new Date(date);
  result.setHours(result.getHours() + hours);
  return result;
}

addHours(date, 5); // 5 hours later
addHours(date, -2); // 2 hours earlier

// Add minutes, seconds, milliseconds
function addMinutes(date, minutes) {
  return new Date(date.getTime() + minutes * 60000);
}

function addSeconds(date, seconds) {
  return new Date(date.getTime() + seconds * 1000);
}

function addMilliseconds(date, milliseconds) {
  return new Date(date.getTime() + milliseconds);
}
```

##### **6.2 Date Differences**

```javascript
/**
 * Calculate difference between two dates
 * @param {Date} date1 - First date
 * @param {Date} date2 - Second date
 * @returns {object} Difference in various units
 */
function dateDifference(date1, date2) {
  const diffMs = Math.abs(date2.getTime() - date1.getTime());

  return {
    milliseconds: diffMs,
    seconds: Math.floor(diffMs / 1000),
    minutes: Math.floor(diffMs / (1000 * 60)),
    hours: Math.floor(diffMs / (1000 * 60 * 60)),
    days: Math.floor(diffMs / (1000 * 60 * 60 * 24))
  };
}

const date1 = new Date('2023-10-01');
const date2 = new Date('2023-10-04');
dateDifference(date1, date2); // { milliseconds: 259200000, seconds: 259200, minutes: 4320, hours: 72, days: 3 }

/**
 * Check if date is in the past/future
 * @param {Date} date - Date to check
 * @returns {string} 'past', 'future', or 'present'
 */
function getDateStatus(date) {
  const now = new Date();
  const diff = date.getTime() - now.getTime();

  if (diff < -1000) return 'past'; // Within 1 second
  if (diff > 1000) return 'future';
  return 'present';
}
```

##### **6.3 Date Comparison**

```javascript
const date1 = new Date('2023-10-04');
const date2 = new Date('2023-10-04');
const date3 = new Date('2023-10-05');

/**
 * Compare dates
 * @param {Date} a - First date
 * @param {Date} b - Second date
 * @returns {number} -1 if a < b, 0 if equal, 1 if a > b
 */
function compareDates(a, b) {
  const timeA = a.getTime();
  const timeB = b.getTime();

  if (timeA < timeB) return -1;
  if (timeA > timeB) return 1;
  return 0;
}

compareDates(date1, date2); // 0 (equal)
compareDates(date1, date3); // -1 (date1 is earlier)

// Check if dates are on the same day
function isSameDay(date1, date2) {
  return date1.getFullYear() === date2.getFullYear() &&
         date1.getMonth() === date2.getMonth() &&
         date1.getDate() === date2.getDate();
}

// Check if date is today
function isToday(date) {
  return isSameDay(date, new Date());
}

// Check if date is within range
function isDateInRange(date, startDate, endDate) {
  return date >= startDate && date <= endDate;
}
```

#### **7. Time Zones and Internationalization**

##### **7.1 Working with Time Zones**

```javascript
// Get user's timezone
const userTimezone = Intl.DateTimeFormat().resolvedOptions().timeZone;
console.log(userTimezone); // e.g., "America/New_York"

// Format date in specific timezone
const nyFormatter = new Intl.DateTimeFormat('en-US', {
  timeZone: 'America/New_York',
  dateStyle: 'full',
  timeStyle: 'long'
});

const tokyoFormatter = new Intl.DateTimeFormat('ja-JP', {
  timeZone: 'Asia/Tokyo',
  dateStyle: 'full',
  timeStyle: 'long'
});

const date = new Date();
nyFormatter.format(date); // "Wednesday, October 4, 2023 at 10:30:45 AM EDT"
tokyoFormatter.format(date); // "2023年10月4日水曜日 23:30:45 JST"
```

##### **7.2 Converting Between Time Zones**

```javascript
/**
 * Convert date to different timezone
 * @param {Date} date - Date to convert
 * @param {string} targetTimezone - Target timezone
 * @returns {Date} Date in target timezone
 */
function convertToTimezone(date, targetTimezone) {
  // This is a simplified version - for production use a library like date-fns-tz
  const utc = date.getTime() + (date.getTimezoneOffset() * 60000);
  const targetOffset = getTimezoneOffset(targetTimezone);
  return new Date(utc + (targetOffset * 60000));
}

// Get timezone offset in minutes
function getTimezoneOffset(timezone) {
  const now = new Date();
  const utcDate = new Date(now.toLocaleString('en-US', {timeZone: 'UTC'}));
  const targetDate = new Date(now.toLocaleString('en-US', {timeZone: timezone}));
  return (targetDate.getTime() - utcDate.getTime()) / 60000;
}
```

##### **7.3 Relative Time Formatting**

```javascript
/**
 * Format relative time (e.g., "2 hours ago")
 * @param {Date} date - Date to format
 * @returns {string} Relative time string
 */
function formatRelativeTime(date) {
  const now = new Date();
  const diffMs = now.getTime() - date.getTime();
  const diffSeconds = Math.floor(diffMs / 1000);
  const diffMinutes = Math.floor(diffSeconds / 60);
  const diffHours = Math.floor(diffMinutes / 60);
  const diffDays = Math.floor(diffHours / 24);

  if (diffSeconds < 60) return 'just now';
  if (diffMinutes < 60) return `${diffMinutes} minute${diffMinutes > 1 ? 's' : ''} ago`;
  if (diffHours < 24) return `${diffHours} hour${diffHours > 1 ? 's' : ''} ago`;
  if (diffDays < 7) return `${diffDays} day${diffDays > 1 ? 's' : ''} ago`;

  return date.toLocaleDateString();
}

const pastDate = new Date(Date.now() - 2 * 60 * 60 * 1000); // 2 hours ago
formatRelativeTime(pastDate); // "2 hours ago"
```

#### **8. Date Validation and Error Handling**

##### **8.1 Validating Dates**

```javascript
/**
 * Check if date is valid
 * @param {Date} date - Date to validate
 * @returns {boolean} True if date is valid
 */
function isValidDate(date) {
  return date instanceof Date && !isNaN(date.getTime());
}

// Usage
const validDate = new Date('2023-10-04');
const invalidDate = new Date('invalid');

isValidDate(validDate); // true
isValidDate(invalidDate); // false

/**
 * Validate date string
 * @param {string} dateString - Date string to validate
 * @returns {boolean} True if string represents valid date
 */
function isValidDateString(dateString) {
  const date = new Date(dateString);
  return !isNaN(date.getTime());
}

// Validate date range
function isDateInRange(date, minDate, maxDate) {
  return date >= minDate && date <= maxDate;
}

// Validate age (must be 18+)
function isAdult(birthDate) {
  const today = new Date();
  const age = today.getFullYear() - birthDate.getFullYear();
  const monthDiff = today.getMonth() - birthDate.getMonth();

  if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birthDate.getDate())) {
    return age - 1 >= 18;
  }
  return age >= 18;
}
```

##### **8.2 Safe Date Operations**

```javascript
/**
 * Safe date arithmetic that handles edge cases
 * @param {Date} date - Base date
 * @param {number} days - Days to add
 * @returns {Date} New date
 */
function safeAddDays(date, days) {
  if (!isValidDate(date)) {
    throw new Error('Invalid date provided');
  }

  const result = new Date(date);
  result.setDate(result.getDate() + days);

  // Check for invalid date (e.g., Feb 30)
  if (result.getDate() !== ((date.getDate() + days) % getDaysInMonth(result))) {
    throw new Error('Invalid date result');
  }

  return result;
}

function getDaysInMonth(date) {
  return new Date(date.getFullYear(), date.getMonth() + 1, 0).getDate();
}
```

#### **9. Performance Considerations**

##### **9.1 Date Object Creation**

```javascript
// Avoid creating Date objects in loops
const start = Date.now();

// Bad - creates new Date objects repeatedly
for (let i = 0; i < 100000; i++) {
  const date = new Date();
  // do something
}

// Good - create once and reuse
const baseDate = new Date();
for (let i = 0; i < 100000; i++) {
  const timestamp = baseDate.getTime() + i * 1000;
  const date = new Date(timestamp);
  // do something
}
```

##### **9.2 Caching Formatters**

```javascript
// Cache Intl.DateTimeFormat instances
const formatters = new Map();

function getFormatter(locale, options) {
  const key = `${locale}-${JSON.stringify(options)}`;
  if (!formatters.has(key)) {
    formatters.set(key, new Intl.DateTimeFormat(locale, options));
  }
  return formatters.get(key);
}

// Usage
const formatter = getFormatter('en-US', { dateStyle: 'long' });
formatter.format(new Date());
```

##### **9.3 Efficient Comparisons**

```javascript
// Use timestamps for comparisons (faster than date methods)
const dates = [/* array of dates */];

// Bad - slower
dates.sort((a, b) => a.getTime() - b.getTime());

// Good - faster
dates.sort((a, b) => a - b); // Implicit getTime() call
```

#### **10. Common Mistakes and Pitfalls**

- **Month indexing**: `new Date(2023, 10, 4)` creates November 4, not October 4
- **Timezone confusion**: `new Date('2023-10-04')` vs `new Date('2023-10-04T00:00:00Z')`
- **Invalid dates**: `new Date('2023-02-30')` creates March 2, not an error
- **DST transitions**: Some hours may be skipped or repeated
- **String parsing**: Avoid ambiguous date formats like '10/04/2023'
- **Mutation**: Date objects are mutable - use `new Date(date)` for copies
- **Comparisons**: Use `getTime()` or timestamps for reliable comparisons
- **Serialization**: Use ISO strings for JSON serialization

#### **11. Modern Alternatives**

##### **11.1 Temporal API (Experimental)**

```javascript
// Temporal is a new modern Date/Time API (not widely supported yet)
// Example usage when available:

// Create dates
const date = Temporal.PlainDate.from('2023-10-04');
const datetime = Temporal.PlainDateTime.from('2023-10-04T14:30:45');

// Arithmetic
date.add({ days: 7 });
datetime.subtract({ hours: 2 });

// Time zones
const zoned = Temporal.ZonedDateTime.from('2023-10-04T14:30:45+05:30[Asia/Kolkata]');
```

##### **11.2 Popular Libraries**

```javascript
// date-fns (recommended)
// npm install date-fns

import { format, addDays, differenceInDays } from 'date-fns';

const date = new Date();
format(date, 'yyyy-MM-dd'); // "2023-10-04"
addDays(date, 7); // Date 7 days later
differenceInDays(date, new Date()); // Number of days difference

// moment.js (legacy but still used)
// npm install moment

const moment = require('moment');
moment().format('YYYY-MM-DD'); // Current date formatted
moment().add(7, 'days'); // 7 days from now
```

#### **12. Practical Examples**

##### **12.1 Countdown Timer**

```javascript
function createCountdown(targetDate) {
  const interval = setInterval(() => {
    const now = new Date().getTime();
    const distance = targetDate.getTime() - now;

    if (distance < 0) {
      clearInterval(interval);
      console.log('Countdown finished!');
      return;
    }

    const days = Math.floor(distance / (1000 * 60 * 60 * 24));
    const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
    const seconds = Math.floor((distance % (1000 * 60)) / 1000);

    console.log(`${days}d ${hours}h ${minutes}m ${seconds}s`);
  }, 1000);

  return interval;
}

const target = new Date('2023-12-31T23:59:59');
createCountdown(target);
```

##### **12.2 Calendar Generation**

```javascript
function generateCalendar(year, month) {
  const firstDay = new Date(year, month, 1);
  const lastDay = new Date(year, month + 1, 0);
  const daysInMonth = lastDay.getDate();
  const startingDayOfWeek = firstDay.getDay();

  console.log(`${firstDay.toLocaleString('default', { month: 'long' })} ${year}`);
  console.log('Su Mo Tu We Th Fr Sa');

  let day = 1;
  for (let week = 0; week < 6; week++) {
    let weekString = '';
    for (let dayOfWeek = 0; dayOfWeek < 7; dayOfWeek++) {
      if ((week === 0 && dayOfWeek < startingDayOfWeek) || day > daysInMonth) {
        weekString += '   ';
      } else {
        weekString += day.toString().padStart(2, ' ') + ' ';
        day++;
      }
    }
    console.log(weekString.trim());
    if (day > daysInMonth) break;
  }
}

generateCalendar(2023, 9); // October 2023
```

##### **12.3 Age Calculator**

```javascript
function calculateAge(birthDate, currentDate = new Date()) {
  if (!isValidDate(birthDate)) {
    throw new Error('Invalid birth date');
  }

  let years = currentDate.getFullYear() - birthDate.getFullYear();
  let months = currentDate.getMonth() - birthDate.getMonth();
  let days = currentDate.getDate() - birthDate.getDate();

  // Adjust for negative months/days
  if (days < 0) {
    months--;
    const lastMonth = new Date(currentDate.getFullYear(), currentDate.getMonth() - 1, birthDate.getDate());
    days += (currentDate.getTime() - lastMonth.getTime()) / (1000 * 60 * 60 * 24);
  }

  if (months < 0) {
    years--;
    months += 12;
  }

  return {
    years: Math.max(0, years),
    months: Math.max(0, months),
    days: Math.max(0, Math.floor(days))
  };
}

const birthDate = new Date('1990-05-15');
const age = calculateAge(birthDate);
console.log(`Age: ${age.years} years, ${age.months} months, ${age.days} days`);
```

#### **13. Summary**

| Category              | Status | Completion |
|-----------------------|--------|------------|
| Date creation         | ✓      | 100%       |
| Date getters/setters  | ✓      | 100%       |
| Date formatting       | ✓      | 100%       |
| Date arithmetic       | ✓      | 100%       |
| Time zones            | ✓      | 100%       |
| Date validation       | ✓      | 100%       |
| Performance           | ✓      | 100%       |
| Common mistakes       | ✓      | 100%       |
| Modern alternatives   | ✓      | 100%       |
| Practical examples    | ✓      | 100%       |

Overall Completion: 100% 📊

Master JavaScript Date and Time handling by understanding the Date object's methods, being aware of timezone complexities, using modern formatting APIs, and avoiding common pitfalls. Always validate dates and consider performance implications in your applications.