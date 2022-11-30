---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.14.1
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

# Check if dl2 files of master and PR are the same

```python
from ctapipe.io.tableloader import TableLoader
import numpy as np

tl_pr = TableLoader("/Users/stefan/Downloads/all.h5", load_dl1_parameters=True)
tl_master = TableLoader("/Users/stefan/Downloads/all_master.h5", load_dl1_parameters=True)

table_pr = tl_pr.read_telescope_events()
table_master = tl_master.read_telescope_events()


keys = table_pr.keys()
keys.remove('tels_with_trigger')
checked_keys = []
for key in keys:
    table_master.remove_rows(np.isnan(table_master[key].value))
    table_pr.remove_rows(np.isnan(table_pr[key].value))
    if np.all(table_master[key]==table_pr[key]):
        checked_keys.append(key)
        
checked_keys == keys
```

```python
len(table_pr)
```

```python

```
