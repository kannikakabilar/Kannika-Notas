<h1 style="color:#4b04c7">Bash</h1>

<h3 style="color:#4b04c7">Intro</h3>

> - <a style="color:#000000">Everyday computer tasks can be done using the concise scripts that Bash can produce</a>

```bash
#!/bin/bash

echo "Hello, World!"
```

> - <a style="color:#000000">Variables</a>

```bash
#!/bin/bash

AGE=25
echo $AGE
readonly AGE
AGE=26
echo $AGE

# Output
# 25
# line 6: AGE: is read-only
```

```bash
#!/bin/bash

AGE=25
echo $AGE
unset AGE
echo "empty":$AGE

# Output
# 25
# empty:
```

> - <a style="color:#000000">Global vs Local Scope</a>

```bash
#!/bin/bash

setAge() {
    echo "Inside Function Age: $AGE"
}
AGE=40
setAge
echo "Script Age: $tmp"

# Output
# Inside Function Age: 40
# Script Age: 40
```

```bash
#!/bin/bash

setAge() {
    local AGE=25
    echo "Local Variable Age: $AGE"
}
AGE=40
setAge
echo "Global Age: $tmp"

# Output
# Local Variable Age: 25
# Global Age: 40
```
