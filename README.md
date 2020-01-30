![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        


# Find Default Logins Quickly With SQL
**Post Date: March 20, 2018**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

![Find Default SQL Logins Quickly With SQL]( https://mikesdatawork.files.wordpress.com/2018/03/image0011.png "Find Default SQL Logins Quickly With SQL")
 
<p>Here's some quick SQL logic which gets you the default logins automatically created at the point of installation, and also those created after the installation was already carried out. It's designed to pull all logins that were created during the first minute of the security setup. Notice the time of creation of the default accounts are all at 11:41 (or earlier as in the default 'sa' account shows)
Keep in mind this only shows logins created whenever you perform a traditional SQL Server Installation without associated services such as Reporting Services, Analysis Services etc.</p> 



## SQL-Logic
```SQL
use master;
set nocount on
 
-- get date when sql server was installed
declare @install_date       datetime = (select [createdate] from syslogins where [sid] = 0x010100000000000512000000)
declare @default_accounts   datetime = (select dateadd(minute, 1, @install_date))
 
-- get all logins not associated with the installed accounts
select [createdate], [name] from syslogins where [createdate] > @default_accounts
 
-- get all default logins created during installation.
select [createdate], [name] from syslogins where [createdate] < @default_accounts
```



[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

 
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

