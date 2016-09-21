# Crontab
Examples explaining crontab lines

## Fields and Allowed Values

```0-59``` minute

```0-23``` hour

```1-31``` day of month

```1-12``` or ```first 3 letters``` month

```0-7``` or ```first 3 letters (0 or 7 is Sun)``` day of week

## Special Characters

```Asterisk (*)``` The Asterisk is used as a wild card, used to specify any occurrence of the field 

```Comma (,)``` The Comma is used when creating a list, to specify 2 or more times of execution

```Hyphen (-)```  The Hyphen is used to specify a range

```Forward Slash (/)```	The Slash is used as an interval, it can be used with a range or wild card to run at a specified interval

```@reboot```  Run once, at startup.

```@yearly or @annually```  Run once a year, equivalent to ```0 0 1 1 *```

```@monthly```  Run once a month, equivalent to ```0 0 1 * * ```

```@weekly```  Run once a week, equivalent to ```0 0 * * 0 ```

```@daily or @midnight```  Run once a day, equivalent to ```0 0 * * * ```

```@hourly```  Run once an hour, equivalent to ```0 * * * * ```

## Examples

Run every Tuesday at 2:30:

```30 2 * * tue /path/to/command``` or ```30 2 * * 2 /path/to/command```

Run every 10 minutes:

```*/10 * * * * /path/to/command```

Run every 2 hours, on the half-hour:
 
```30 */2 * * * /path/to/command```
 
Run every 2 hours on the half-hour, but only on weekdays:
 
```30 */2 * * 1-5 /path/to/command```
 
Run at 12:05, 13:05, ..., and 18:05 :
 
```5 12-18/2 * * * /path/to/command```
 
Run on the first day of every month, at 12:00am :
 
```0 0 1 * * /path/to/command```

Run on the first day of every third month, at 12:00am :

```0 0 1 */3 * /path/to/command```

Execute /path/to/command when the system starts:

```@reboot /path/to/command```
