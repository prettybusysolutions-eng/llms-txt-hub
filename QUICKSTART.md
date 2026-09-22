# Use the directory snapshot

The immediately usable artifact is [`data/websites.json`](data/websites.json).
It is a generated catalog, not a hosted-service deployment or proof that every
linked endpoint is still available.

From a checkout, use Python 3 (no credentials or package installation):

```bash
python3 - <<'PY'
import json
from pathlib import Path
entries = json.loads(Path('data/websites.json').read_text())
assert isinstance(entries, list) and entries
for entry in entries[:5]:
    print(entry['name'], entry['llmsTxtUrl'])
print(f'{len(entries)} directory entries loaded')
PY
```

Expected: five names/URLs and a positive entry count. This reads only local
files; it does not contact the listed sites. Validate remote content before
using it as model context. The catalog does not grant rights to third-party
site content or enforce access controls on models.

Pin the Git commit when consuming this snapshot. To contribute, edit source
MDX under `packages/content/data/websites/`; do not manually edit generated
JSON. See [contribution instructions](.github/CONTRIBUTING.md) and preserve
[upstream attribution](NOTICE.md). Building the full web app has separate
provider/environment requirements; this path deliberately evaluates the data.
