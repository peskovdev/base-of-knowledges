# Looking for name of char
1. Execute in terminal
    ```
    xev | awk -F'[ )]+' '/^KeyPress/ { a[NR+2] } NR in a { printf "%-3s %s\n", $5, $8 }'
    ```
2. Press your keys and see result
