```shell
$fso = New-Object -ComObject Scripting.FileSystemObject

Get-ChildItem -Directory | 
    Select-Object @{Name='Size'; Expression={$fso.GetFolder($_.FullName).Size}}, FullName |
    Sort-Object Size -Descending | 
    Format-Table @{Name='Size'; Expression={
        switch ($_.Size) {
            { $_ -gt 1TB } { '{0:0.0} TeB' -f ($_ / 1TB); break }
            { $_ -gt 1GB } { '{0:0.0} GiB' -f ($_ / 1GB); break }
            { $_ -gt 1MB } { '{0:0.0} MiB' -f ($_ / 1MB); break }
            { $_ -gt 1KB } { '{0:0.0} KiB' -f ($_ / 1KB); break }
            default { '{0:0.0} bytes' -f $_ }
        }
    }}, FullName

```
