---
id: u2p65grcp8aq7hhiqiwm9d9
title: Makefile
desc: ''
updated: 1655489661254
created: 1655489655737
---

Colors

http://jamesdolan.blogspot.com/2009/10/color-coding-makefile-output.html
https://www.shellhacks.com/bash-colors/

```bash
NO_COLOR=\e[0m
OK_COLOR=\e[32m
ERROR_COLOR=\e[31m
WARN_COLOR=\e[33m

OK_STRING=$(OK_COLOR)[OK]$(NO_COLOR)
ERROR_STRING=$(ERROR_COLOR)[ERRORS]$(NO_COLOR)
WARN_STRING=$(WARN_COLOR)[WARNINGS]$(NO_COLOR)

ac:
	@echo -e "$(OK_STRING)"
```