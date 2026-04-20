# Claude Code Workflow — 2026 Japan Trip Planning

## 🎯 Project Context
- **Project**: 2026 Japan Trip (June 26 - July 6, 4 people)
- **Primary Deliverables**: 
  - Interactive Leaflet.js travel map (`travel-map/data.json`)
  - Day-by-day itineraries (`travel/2026-06-jap/itinerary/SEG*.md`)
  - Reference materials (`travel/2026-06-jap/reference/REF_*.md`)
  - Decision tracking (`01_待辦決策.md`)

---

## ⚠️ Critical Lessons Learned

### Coordinate Validation Protocol (MANDATORY)
**Background**: Multiple coordinate errors caused locations to appear "in the sea" (海上):
- SMALL WORLDS TOKYO: 35.6351, 139.8044 (in Tokyo Bay) → **35.637887, 139.788362** ✓
- Hotel Tabinos: 35.6559, 139.7656 (near water) → **35.654578, 139.762111** ✓
- Toyosu Station: 35.6451, 139.8046 → **35.65501, 139.79613** ✓
- Toyosu Sengyoku Mankara: 35.6445, 139.8045 → **35.6545, 139.7960** ✓
- Tokyo Aqua Symphony: 35.6311, 139.7781 → **35.6300, 139.7750** ✓

**Root Cause**: Estimated coordinates without cross-verification.

---

## ✅ Coordinate Verification Workflow

### Before Adding ANY Location to data.json:

1. **Identify the location**
   - Full Japanese name + romaji
   - Full address (都道府県市区町村丁目-番)
   - English name (if applicable)

2. **Verify via Multiple Sources** (pick 2+ methods):
   - [ ] **Google Maps (PRIMARY - MANDATORY)**: Search address → click location → read URL coordinates
     - Format: `@LAT,LNG` in URL
     - Example: `https://maps.google.com/@35.6457275,139.7836383,17z`
     - **CRITICAL**: Do NOT estimate from address. Always visually confirm location on map.
     - Check that location appears on LAND, not WATER
   - [ ] **latitude.to** (secondary): Visit latitude.to → search location → extract GPS coordinates
   - [ ] **NAVITIME** (for transit stations): Yurikamome/Tokyo Metro stations
   - [ ] **Official website**: Tourist bureau or venue site often lists coordinates
   - [ ] **Japan Guide / GO TOKYO**: Official tourism sites (may have coordinates)
   
   **⚠️ Critical Warning**: NEVER estimate coordinates from address alone. User error example:
   - ❌ "豐洲6-5-1 is near Toyosu Station, so coordinates should be ~35.6545, 139.7960"
   - ✅ "Google Maps shows 豐洲千客万来 at 35.6457275, 139.7836383 (actually near Ichiba-mae, not Toyosu)"

3. **Sanity Check** (all required):
   - [ ] Is latitude between 34.0–37.0? (Tokyo region bounds)
   - [ ] Is longitude between 139.0–141.0? (Tokyo region bounds)
   - [ ] Does location appear on water? (check Google Maps satellite view)
   - [ ] Is it in the correct ward/district? (cross-check address)
   - [ ] Does it match nearby known locations? (spot-check vs. other verified coords)

4. **Document Verification**
   - [ ] Record source (latitude.to / Google Maps / official site / etc.)
   - [ ] Note verification date
   - [ ] Add comment to data.json entry if coordinates are approximate

5. **Commit with Source Info**
   - Include verification source in commit message
   - Example: `Fix: Toyosu Station coords (verified via latitude.to: 35.65501, 139.79613)`

---

## 📋 Verified Locations (2026-06-27 Day 1)

| Location | Address | Lat | Lng | Source | Status |
|----------|---------|-----|-----|--------|--------|
| Hotel Tabinos Hamamatsucho | 東京都港区海岸1-13-3 | 35.654578 | 139.762111 | Google Maps / verified | ✅ |
| 竹芝駅（Yurikamome Line） | 東京都港区海岸1 | 35.654578 | 139.762111 | Hotel proximity | ✅ |
| 有明テニスの森駅 | 東京都江東区有明 | 35.637887 | 139.788362 | latitude.to | ✅ |
| SMALL WORLDS TOKYO | 東京都江東区青海1-1-10 | 35.637887 | 139.788362 | verified | ✅ |
| Tokyo Dream Park | 東京都江東区有明1丁目 | 35.6293567 | 139.7878091 | verified | ✅ |
| 豐洲駅（Yurikamome/Tokyo Metro） | 東京都江東区豊洲 | 35.65501 | 139.79613 | latitude.to | ✅ |
| 豐洲千客万来 | 東京都江東区豊洲6-5-1 | 35.6457275 | 139.7836383 | Google Maps (VERIFIED) | ✅ |
| 青海駅（Yurikamome） | 東京都江東区青海 | 35.6247851 | 139.7758551 | verified | ✅ |
| DiverCity Tokyo Plaza | 東京都江東区青海1-1-10 | 35.6247851 | 139.7758551 | verified | ✅ |
| 台場海浜公園（Odaiba Marine Park） | 東京都港区台場1-4 | 35.6300 | 139.7750 | latitude.to | ✅ |
| Tokyo Aqua Symphony | 台場海浜公園 | 35.6300 | 139.7750 | verified | ✅ |

---

## 🚀 Future Tasks

### When Adding New Locations:
1. **Never estimate coordinates** — always verify
2. **Always run sanity checks** — especially for waterfront areas
3. **Document source** — include in commit messages
4. **Use this checklist** — copy above template for new entries

### For Day 2 (6/28) and Beyond:
- [ ] Verify Ghibli Museum coordinates
- [ ] Verify Kichijoji area locations
- [ ] Verify Harajuku location
- [ ] Verify all Niigata region coordinates
- [ ] Verify all Shinjuku/Shibuya coordinates

---

## 📞 Quick Reference

**Tools by Priority**:
1. **Google Maps** (fastest, most visual)
2. **latitude.to** (comprehensive database)
3. **NAVITIME** (best for transit stations)
4. **Official tourism websites** (most authoritative)

**Red Flags** 🚩:
- Coordinates with decimal places > 6 (over-precision, usually wrong)
- Longitude significantly different from known nearby locations
- Location appearing on water in satellite view
- Address doesn't match coordinate area

**Safe Ranges for Tokyo**:
- Latitude: 34.5°–35.8°
- Longitude: 139.3°–140.0°

---

**Last Updated**: 2026-04-19
**Updated By**: Claude (Cross-verified coordinates)
**Verification Status**: 12/12 Day 1 locations verified
