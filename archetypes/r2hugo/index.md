+++
title = "{{ replace .Name "-" " " | title }}"
description = ""
categories = []
tags = []
date = {{ .Date }}
draft = true
+++

{{% include "{{ .File.Dir }}content.md" %}}