# 如下
   * 百度地图4.0以上版本让所有的点都能出现在视图内
   
   ```
      //必须在此接口调用之后完成
           mBaiduMap.setOnMapLoadedCallback(new BaiduMap.OnMapLoadedCallback() {
               @Override
               public void onMapLoaded() {
                   builder = new MapStatus.Builder();
   //                builder.target(target).zoom(8f);
                   mBaiduMap.animateMapStatus(MapStatusUpdateFactory.newMapStatus(builder.build()));
   
                   MarkerOptions oStart = new MarkerOptions();//地图标记覆盖物参数配置类
                   oStart.position(latLngs.get(0));//覆盖物位置点，第一个点为起点
                   oStart.icon(startBD);//设置覆盖物图片
                   oStart.zIndex(1);//设置覆盖物Index
                   mBaiduMap.addOverlay(oStart); //在地图上添加此图层
   
                   //添加终点图层
                   MarkerOptions oFinish = new MarkerOptions().position(latLngs.get(latLngs.size() - 1)).icon(finishBD).zIndex(2);
                   mBaiduMap.addOverlay(oFinish);
   
                   OverlayOptions ooPolyline = new PolylineOptions().width(13).color(getResources().getColor(R.color.colorPrimary)).points(latLngs);
                   mPolyline = (Polyline) mBaiduMap.addOverlay(ooPolyline);
                   
                   //下面代码是将点展示在地图中的关键代码
                   LatLngBounds.Builder builder = new LatLngBounds.Builder();
                   for (LatLng p : latLngs) {
                       builder = builder.include(p);
                   }
                   LatLngBounds latLngBounds = builder.build();
                   MapStatusUpdate u = MapStatusUpdateFactory.newLatLngBounds(latLngBounds, mMapView.getWidth(), mMapView.getHeight());
                   mBaiduMap.animateMapStatus(u);
                   mPolyline.setZIndex(3);
               }
           });
   ```

              
   


