Here's what the script does and what to know before running it:

**How it works**

`Request-SPOPersonalSite` is the SPO Admin cmdlet that triggers OneDrive provisioning server-side for a given UPN. It does not require the user to log in or interact with anything. The `-NoWait` flag submits the request asynchronously so the script doesn't block on each user.

**Prerequisites**

- The `Microsoft.Online.SharePoint.PowerShell` module must be installed (`Install-Module Microsoft.Online.SharePoint.PowerShell`)
- The account running the script must be a **SharePoint Administrator** or **Global Administrator**
- Modern Auth / MFA is supported through `Connect-SPOService`

**Before running**

Update these three lines at the top of the script to match your environment:
- `$CsvPath` — path to your UPN list
- `$AdminUrl` — your tenant's SPO admin URL (`https://[tenant]-admin.sharepoint.com`)
- `$LogPath` — where you want the run log written

**CSV format expected**

```
UserPrincipalName
jsmith@contoso.com
adoe@contoso.com
```

**After running**

Provisioning is queued asynchronously by Microsoft — sites typically become active within **a few minutes**, though in large tenants it can take longer. The optional verification block at the bottom of the script can be uncommented and run separately once you're ready to confirm the sites are live before kicking off your migration jobs.
