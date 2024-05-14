```shell
gci -Directory `
| select @{l='Size'; e={$fso.GetFolder($_.FullName).Size}},FullName `
| sort Size -Descending `
| ft @{l='Size'; e={'{0:N2}    ' -f (&{If($_.Size -gt 1KB){If($_.Size -gt 1MB){If($_.Size -gt 1GB){'{0:0.0} GiB' -f ($_.Size/1GB)}Else{'{0:0.0} MiB' -f ($_.Size/1MB)}}Else{'{0:0.0} KiB' -f ($_.Size/1KB)}}Else{"{0:0.0} bytes" -f ($_.Size)}})}},FullName
```
