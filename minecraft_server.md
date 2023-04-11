root@ultra:/etc/systemd# grep -r spigot *
system/minecraft.service:ExecStart=/usr/bin/java -Xmx1024M -Xms1024M -jar spigot.jar --noconsole

apache-maven-3.6.0  BuildData  BuildTools.jar  BuildTools.log.txt  Bukkit  CraftBukkit  lastbuild.log  lastdl.log  Spigot  update.sh  work
minecraft@ultra:~/build/spigot$ ./update.sh

minecraft@ultra:~/server$ mv ../build/spigot/spigot-1.18.jar bundler/
libraries/ versions/


minecraft@ultra:~/server$ mv bundler/versions/spigot-1.18.jar ./spigot.jar

