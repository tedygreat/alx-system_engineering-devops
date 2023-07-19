## 0x13 fire wall
# check if ufw is installed or enabled

$ sudo ufw status

# if the result shows enabled then disable it
$ sudo ufw disable

# configuring firwall rules
$ sudo ufw default deny incoming
$ sudo ufw default allow outgoing
$ sudo ufw allow 22/tcp		/to enable ssh connection
$ sudo ufw allow 80/tcp		/to enable connection on port 80
$ sudo ufw allow 443/tcp	/to enable conection on port 443
$ sudo ufw enable

# enabling port forwarding via UFW

# add this below rule to the /etc/ufw/before.rules file
# make sure its before the *filter line, VERY IMPORTANT

*nat
: PREROUTING ACCEPT [0:0]
-A PREROUTING -p tcp --dport 8080 -j REDIRECT --to-port 80
COMMIT

# Then go to your /etc/sysctl.conf file to enable port forwarding by
# uncommenting the line #net.ipv4.ip_forward=1

-- before
#net.ipv4.ip_forward=1

--after
net.ipv4.ip_forward=1

# then reload the sysctl configuration
$ sudo sysctl -p

# congratulations !! you've done it
# if this is confusing, then watch the video above to get it done yourself.
