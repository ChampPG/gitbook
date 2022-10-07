# Console Into Cisco Device

### Steps to Setup Computer

1. After connection to the console port open `Device Manager`
   1. Take now of the COM\<Num> is. This will be used later in the PuTTY config
2. You want the setting to be the same as the table below

| Variable     | Value |
| ------------ | ----- |
| Bits per sec | 9600  |
| Data bits    | 8     |
| Parity       | None  |
| Stop bits    | 1     |
| Flow Control | None  |

&#x20; 3\. Now open PuTTY and navigator to `Serial` under `SSH`

<figure><img src="../.gitbook/assets/Screenshot 2022-09-24 145237.png" alt=""><figcaption><p>Shows the PuTTY config</p></figcaption></figure>

&#x20; 4\. Now under Session Select the COM\<Num> from earlier

<figure><img src="../.gitbook/assets/Screenshot 2022-09-24 145607.png" alt=""><figcaption><p>Session Config</p></figcaption></figure>

&#x20; 5\. Click `Open` and if everything was setup properly you should be in the CISCO CLI
