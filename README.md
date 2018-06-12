An openshift deployment of review-rot

https://github.com/nirzari/review-rot/pull/44

---

Updating this project is ridiculous.

Edit the hidden secrets/configuration.yaml file to your heart's content, and then:

```bash
oc delete secrets/reviewrot-config
oc secret new reviewrot-config ./secret/configuration.yaml
```
