Map.centerObject(geometry)

var time_start= "2015", time_end= "2021"

var landsat = imageCollection
.filterDate(time_start, time_end)
.filter(ee.Filter.lt('CLOUD_COVER',10))
.filter(ee.Filter.calendarRange(6,12,'month'))
.filterBounds(geometry).map(function(img){
  var bands = img.select("SR_.*").multiply(2.75e-05).add(-0.2);
  var ndwi = bands.normalizedDifference(['SR_B3','SR_B5']).rename("ndwi");
  return ndwi
  .copyProperties(img, img.propertyNames())
  
}).median();

Map.addLayer(landsat.clip(geometry), [],'ndwi_summer',false)
Map.addLayer(landsat.clip(geometry).gt(0), [], 'ndwi_thr', false);
var thr = landsat.gt(0.3);
var mask = thr.updateMask(thr);

Map.addLayer(mask, [], 'ndwi_masked', false);


var pixel_area = mask.multiply(ee.Image.pixelArea().divide(1e6));

Map.addLayer(pixel_area.clip(geometry), [], 'ndwi_pixel_area', false);

var lake_area = pixel_area.reduceRegion({
  reducer: ee.Reducer.sum(), geometry: geometry, scale: 100
  }).values().get(0);
  
  
print(ee.Number(lake_area))
