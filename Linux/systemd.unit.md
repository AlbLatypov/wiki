[Unit]
Description=Mount_fs_for_backup
Documentation=http://example.org/
After=network.target

[Service]
WorkingDirectory=/root/backup
ExecStart=/root/backup/mnt-fs.sh
KillMode=mixed
Restart=on-failure
Type=simple

[Install]
WantedBy=multi-user.target
Alias=mnt-backup.service


/etc/systemd/system/mnt-backup.service
