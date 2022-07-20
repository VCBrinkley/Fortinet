## Trustwave Fortinet Whitelisting

Navigate to http://192.168.90.10

Locate Fortinet FW serial number, copy the contents under the **Name** header

Click the hyperlink located far right under the **Manager** header

Select **Device Manager** from the dashboard

On the bottom left of the page there is a search bar, paste the **Name** and select it

Under **Configuration and Installation Status** select **Database Configuration** and click the **View** option

Search for urlfilter and verify what edit # it's associated with

Verify if the website has already been whitelisted by searching for the website in the device configuration.

![](e.png)

> If the website is whitelisted in the configuration no configuration is needed.

If the website isn't whitelisted, select **Telnet** located under **Connection Summary** on the **System Dashboard**

![](bb2.png)

Enter your admin credentials and you should be ready to begin, the following commands can be copy and pasted into the terminal

![](none.png)

`config webfilter urlfilter`

`edit 1` (in this case our urlfilter is associated with **1**)

`config entries`

![](none2.png)

`show`

![](show1.png)

This shows us the full list of whitelisted urls, since I'm going to add a new whitelisting, the next number will be 383

`edit 383` (creating whitelist entry)

`set url yelp.nowait.com` (yelp.nowait.com is my target url for whitelisting)

`set action allow`

`next`

`show` (verify the url has been added to the list)

`move 383 before 10000` (places the whitelist above the deny all)

`show` (verify the url is above 10000)

`end`

`end`

The device should have the url whitelisted now, exit **Telnet**

### Wildcard Whitelisting

`config webfilter urlfilter`

`edit 1`

`config entries`

`edit 384`

`set url *.nowitapp.com` (example url, * is the wildcard)

`set type wildcard` 

`next`

`move 384 before 10000`

`show` (verify its added)

`end`

`end`

The device should have the url whitelisted under Wildcard rules, exit **Telnet**











