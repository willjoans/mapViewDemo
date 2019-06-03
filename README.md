# mapViewDemo

import GoogleMaps
import GooglePlaces

GMSPlacesClient.provideAPIKey("AIzaSyAcyvOKnjeF8KknkLIoyzCB6Ww2yjoSqgU")
GMSServices.provideAPIKey("AIzaSyANVfVloe00YyajPv0Rs8YN4_N-V8JzACY")


  Bean.latitude = TO_STRING(ClientBean["latitude"]as AnyObject)
  Bean.longitude = TO_STRING(ClientBean["longitude"]as AnyObject)
                           
    let position = CLLocationCoordinate2D(latitude: TO_DOUBLE(Bean.latitude),longitude: TO_DOUBLE(Bean.longitude))
                            self.mapView.camera = GMSCameraPosition.camera(withTarget: position, zoom:10)
                            self.mapView.isMyLocationEnabled = true
                            let marker = GMSMarker(position: position)
                            marker.icon = UIImage(named:"map_marker")
                            marker.tracksViewChanges = true
                            marker.map = self.mapView
                            marker.title = Bean.Name
                            marker.snippet = Bean.clientlocation
                            marker.zIndex = Int32(self.mapAnnotationtag)
                            self.mapAnnotationtag += 1
                           self.MapArrray.append(Bean)
                           
                           
    func mapView(_ mapView: GMSMapView, didTapInfoWindowOf marker: GMSMarker) {
       let Bean = MapArrray[Int(marker.zIndex)]
        let CateGoryDetailVC = UISTORYBORD.SBUSERBORD.instantiateViewController(withIdentifier: "CateGoryDetailVC")as! CateGoryDetailVC
        CateGoryDetailVC.completeclientid = Bean.completeclientid
        self.navigationController?.pushViewController(CateGoryDetailVC, animated: true)
        
    }
    
    
    ==============================================================
    @IBOutlet var mapView: GMSMapView!
    let locationManager = CLLocationManager()
    var lat  = Double()
    var long  = Double()
    
    
    
    locationManager.delegate = self;
        locationManager.desiredAccuracy = kCLLocationAccuracyBest
        locationManager.requestAlwaysAuthorization()
        locationManager.startUpdatingLocation()
        
        let position = CLLocationCoordinate2D(latitude:24.965695, longitude: 55.060585)
        
        self.mapView.camera = GMSCameraPosition.camera(withTarget: position, zoom:11.5)
        self.mapView.isMyLocationEnabled = true
        self.mapView.setMinZoom(11.7, maxZoom: self.mapView.maxZoom)
        let marker = GMSMarker(position: position)
        //marker.icon = UIImage(named:"placeholder")
        marker.tracksViewChanges = true
        marker.title = "CableDeport"
        marker.map = self.mapView
      
       func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        let locValue:CLLocationCoordinate2D = manager.location!.coordinate
        lat = locValue.latitude
        long = locValue.longitude
        print(lat)
        print(long)
    }
    ===================================================================
    
     let url = URL(string: "http://maps.google.com/?saddr=\(lat),\(long)&daddr=\(24.965695),\(55.060585)&dirflg=d")!
        
        if #available(iOS 10.0, *) {
            UIApplication.shared.open(url, options: [:], completionHandler: nil)
        }
        else
        {
            UIApplication.shared.openURL(url)
        }
        =======================================================
        
        
