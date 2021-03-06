### 0.5.0
- loadtimeout adaptive

### 0.5.1
- optimize loadtimeout adaptive

### 0.5.2
- fix bug when re-instantiate Hls, signaling is switched to default setting

### 0.5.3
- fix a bug may block p2p
- max buffer size setting for mobile

### 0.5.4
- detect and report player

### 0.6.0
- pre-buffer for smooth playing
- Add new field `live`

### 0.7.0
- Add `validateSegment` [funtion](https://docs.cdnbye.com/#/en/API?id=how-to-check-segment-validity)

### 0.8.0
- Add `prefetchHttpSegments`: The number of segments that will be forced to download by HTTP at the beginning
- Add `getStats`function in p2pConfig

### 0.8.1
- Restart P2P if the node expired
- Increase buffer size

### 0.9.0
- Optimize P2P algorithm
- Solved the buffer stall problem in live

### 0.9.1
- Fix data reporting bug
- Remove `prefetchHttpSegments`

### 0.9.2
- Parameter optimization
- Fixed bugs in clappr-plugin

### 0.9.4
- live mode optimization
- fix known bug

### 0.10.2
- Optimize P2P algorithm
- fix data report bug

### 0.10.5  13/8/2019
- live mode optimization
- fix known bug

### 0.11.0 20/8/2019
- Optimize P2P algorithm

### 0.11.1-0.11.2 25/8/2019
- fix bug when using encrypted hls

### 0.12.0 12/9/2019
- Optimize P2P algorithm
- Prevent repeated loads of cdnbye

### 0.12.2 3/10/2019
- vod mode p2p optimization
- fix known bug

### 0.12.3 14/10/2019
- Optimize play experience
- fix known bug

### 0.13.2 4/11/2019
- Use http range requests if possible
- fix known bug

### 0.13.4 10/12/2019
- Optimize parameters
- fix known bug

### 0.14.0 23/12/2019
- Update hls.js to 0.13.0

### 1.0.0 4/1/2020
- Release v1.0.0
- `useHttpRange` is not available by default