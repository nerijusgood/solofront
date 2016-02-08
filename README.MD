#Solofront Grav theme

## Setup

Download latest release: (get url [here](https://github.com/getgrav/grav/releases "GetGrav Github"))
`wget https://github.com/getgrav/grav/releases/download/1.0.6/grav-v1.0.6.zip`

Unzip:
`unzip zip`

Rename folder to whatever you want on server:
`mv grav solofront.com`

Move folder to desired folder on *server*:
`scp -r solofront.com nerijusg@nerijusgood.com:~/public_html/`

ssh to server and install plugins/updates:
`bin/grav install`
