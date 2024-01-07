# Mobile Security Framework(MobSF)
## MobSF in Docker
### Setting Up
```
docker pull opensecurity/mobile-security-framework-mobsf:latest
```
```
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

### Upload the APK
```
curl -F 'file=@goatdroid.apk' http://localhost:8000/api/v1/upload -H "Authorization:[Token]"
```

Review uploaded file at http://127.0.0.1:8000/recent_scans
### Scan the APK
```
curl -X POST --url http://localhost:8000/api/v1/scan --data "scan_type=apk&file_name= goatdroid.apk&hash= 969bac4cb8392ceb79b5e60f310e480b" -H "Authorization:[Token]
```
### Download report
```
curl -X POST  --url  http://localhost:8000/api/v1/download_pdf  --data "hash=969bac4cb8392ceb79b5e60f310e480b&scan_type=apk" -H "Authorization:563d64fc5054d3b239ac0419f1d6b2378465f5c80e1778c283eb1e3265bdd7ae"  >  MobSFTest.pdf
```

## MobScan
* pip install mobsfscan
* mobsfscan tests/assets/src/

### MobScan in Docker
* docker pull opensecurity/mobsfscan
* docker run -v /path-to-source-dir:/src opensecurity/mobsfscan /src

ดูรายละเอียดการใข้งาน [Mobscan](https://github.com/MobSF/mobsfscan)