# helm-charts-releaser

* [testrtc-speedtest](https://bd-spl.github.io/helm-charts-releaser/charts/testrtc-speedtest/)

## Releasing a testrtc-speedtest build (if you are John Doe)

Make changes, prepare for a release, poke the version in `Chart.yaml`, commit it.
It is now ready to build with
[chart-releaser](https://github.com/helm/chart-releaser), will publish to
`https://<johndoe>.github.io/helm-charts-releaser/charts/testrtc-speedtest/`:
```
cat > ~/.cr.yaml << EOF
owner: johndoe
git-repo: helm-charts-releaser
package-path: .cr-release-packages
# use your valid github API token
token: ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
git-base-url: https://api.github.com/
git-upload-url: https://uploads.github.com/
EOF

pip install --user yq
cd charts/testrtc-speedtest

# TODO: it's not clear how to poke versions and upload only new version
VERSION=$(yq -r '.version' Chart.yaml)

cr package --sign --keyring ~/.gnupg/secring.gpg \
     --key 'John Doe <johndoe@email.org' --config ~/.cr.yaml
cr upload --skip-existing --config ~/.cr.yaml

# FIXME: it panics in the end, but generates index.yaml.
# Then all consequent indexer executions fail:
#   Error: .cr-release-packages/speedtest-x.y.z.tgz.prov is not
#   a helm chart package: file '.cr-release-packages/speedtest-x.y.z.tgz.prov'
#   does not appear to be a gzipped archive; got 'text/plain; charset=utf-8'

cr index --pages-index-path index.yaml -i index.yaml -p .cr-release-packages --config ~/.cr.yaml
```
Commit generated `index.yaml` and cherry-pick it into `gh-pages` branch's root dir as well.
```
mv index.yaml ../../
git add ../../index.yaml
git commit -m Index
git push
git checkout gh-pages
git cherry-pick <use the above commit id>
git push
```
In the helm-charts-releaser repo settings for github pages, make sure it is generated
from the `main` branch, where is README file located. The branch `gh-pages` is
only needed for chart releaser indexer, and helm CLI to fetch `index.yaml`
provided with it.
