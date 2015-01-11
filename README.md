Isilon_Tools
=============
  The script utilizing Isilon Platform API interface to back up shares, exports and quotas for use cases such as: DRP and backup   necessaryconfiguration for DR. 
<hr>

### Summary
  EMC Isilon scale-out storage solutions are designed for the enterprise that want to manage their data, not their storage. Our storage systems are powerful yet simple to install, manage, and scale to virtually any size. And, unlike traditional enterprise storage, Isilon solutions stay simple no matter how much storage capacity is added, how much performance is required, or how business needs change in the future. We’re challenging enterprises to think differently about their storage, because when they do, they’ll recognize there’s a better, simpler way – with Isilon.
  The script utilizing Isilon Platform API interface to back up shares, exports and quotas for use cases such as: DRP and backup necessary configuration for DR.

### Install
  Create and restore shares, exports and quotas on an Isilon system utilizing the REST API interface. 
  This script was written against Python 2.7.8 and will require the requests (2.4.3 or newer) package to be installed using:<br>
  
      pip install requests
      pip install requests --upgrade (if using an older version of requests)
  The script has been tested on python 2.6 on both Linux (FreeBSD – Isilon OS) and windows 7 with OneFS 7.0.x and 7.1.x.

### Usage
      usage: isi_tools.py [-h] [-v] [-f FILE] -t TYPE -u USER -pw PASSWORD -n
            CLUSTERNAME
            backup | restore --file FILE
      optional arguments:
          -h, --help            show this help message and exit
          -v, --verbose         detailed logging.
      Actions:
          backup | restore --file FILE
                        backup/restore the object is selected on the –type flag
      Required:
          -t TYPE, --type TYPE  specifies the type of the object [shares, export, quotas].
          -f FILE, --file FILE  Path to the backup file for restore operaiotn.
          -u USER, --username USER
                        Username for login.
          -pw PASSWORD, --password PASSWORD
                        Password to login.
          -n CLUSTERNAME, --name CLUSTERNAME
                        Cluster name to connect.

### Arguments
      Backup			Backup Action.
      Restore    	Restore action.
### Options
      -h --help               Show this help screen
      -v, --verbose          	For detailed log and messages.
      -t, --type		Path to the backup file for restore operation. (required ONLY for restore operation)
      -u, --user		Username for Isilon API.
      -pw, --password			Password for Isilon API.
      -n, --name		Cluster name or IP of the Isilon system.

### Running Isilon Tools
* The default path for the backup file is “./archive”, in case the path is not exist the backup file will be saved on the current directory.

* The name of the backup file is build from the type and date&time which the file was created. For example: quotas_29_12_18_11.bck is back file of quotas which was taken on December 29 in 6:11.

        isi_tools.py backup --user root --password a --name 10.64.94.160 --type shares
![alt tag](https://github.com/obergt/Isilon_Tools2/blob/master/images/backup_shares.png)

        isi_tools.py backup --user root --password a --name 10.64.94.160 --type exports
![alt tag](https://github.com/obergt/Isilon_Tools2/blob/master/images/backup_exports.png)

        isi_tools.py backup --user root --password a --name isi-lab.ps --type quotas
![alt tag](https://github.com/obergt/Isilon_Tools2/blob/master/images/backup_quotas%5Bwith%20cluster%20name%5D.png)

        isi_tools.py restore --user root --password a --name isi-lab.ps --type exports --file ./archive/exports_29_12_18_9.bck
![alt tag](https://github.com/obergt/Isilon_Tools2/blob/master/images/restore_exports.png)
        
*Note: As you can see in the screenshot above an error returned while the script was tried to create an export. This is OK, the script is just raising the API error he gets in case of an exception, In this case the export which I was trying to create is already exist.*

### Use Cases & Recommendations
**For replications:**<br>
My recommendation is to schedule this script to back up your system configuration with the backup operation and use SyncIQ (if you have license) or other method to move the .bck files to the remote system.<br> 
Restore the backup file on the remote system only on the time of the failover and on schedule.

**For Back up:**<br>
Schedule the script to back up your system configuration and save it somewhere else (Not only on the Isilon system).

### Contributing
Please contribute in any way to the project.

### Licensing
Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an “AS IS” BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

### Support
Please file bugs and issues at the Github issues page. For more general discussions you can contact the EMC Code team at Google Groups. The code and documentation are released with no warranties or SLAs and are intended to be supported through a community driven process.