# Data Mapping vs. ACEA and other APIs

ACEA has created a level A1 proposal for a predefined data list. This document describes how these datapoints match current VSS specification.

As a reference it also include comparison with APIs presented by OEMs:
* Volvo:<https://developer.volvocars.com/volvo-api/extended-vehicle/#Resources>
* Mercedes:<https://developer.mercedes-benz.com/products/connect_your_fleet/details>
* Android: <https://android.googlesource.com/platform/hardware/interfaces/+/master/automotive/vehicle/2.0/types.hal>

<table>
  <tr>
    <th>ACEA</th>
    <th>VSS</th>
    <th>Comment</th>
    <th>Volvo</th>
    <th>Mercedes</th>
    <th>Android</th>
  <tr>
    <td>1. Speed of Vehicle</td>
    <td>Vehicle.Speed (km/h)</td>
    <td>Duplicate: Vehicle.OBD.Speed, Deprecated:Vehicle.Cabin.Infotainment.Navigation.CurrentLocation.Speed, Vehicle.Powertrain.Transmission.Speed</td>
    <td>-</td>
    <td>Driving.Speed.Current (km/h)</td>
    <td>PERF_VEHICLE_SPEED (m/s), PERF_VEHICLE_SPEED_DISPLAY (m/s)</td>
  </tr>
  <tr>
    <td>2. Acceleration of Vehicle</td>
    <td>Vehicle.Acceleration.Longitudinal (m/s²)</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
  </tr>
  <tr>
    <td>3. Odometer Value</td>
    <td>Vehicle.TravelledDistance (km) </td>
    <td>Duplicate: Vehicle.Powertrain.Transmission.TravelledDistance</td>
    <td>odometer (km)</td>
    <td>Driving.Odometer.Lifetime (km)</td>
    <td>PERF_ODOMETER (km)</td>
  </tr>
  <tr>
    <td>4. Diagnostic Trouble Codes</td>
    <td>Vehicle.OBD.Status.DTCCount, Vehicle.OBD.DriveCycleStatus.DTCCount </td>
    <td>-</td>
    <td>-</td>
    <td>e.g. InternalCombustionEngine.LimpMode.IsActive</td>
    <td>OBD2_FREEZE_FRAME, OBD2_FREEZE_FRAME_INFO?</td>
  </tr>
  <tr>
    <td>5. Vehicle high voltage Battery State of Charge</td>
    <td>Vehicle.Powertrain.Battery.StateOfCharge.Current, Vehicle.Powertrain.Battery.StateOfCharge.Displayed (percent)</td>
    <td>-</td>
    <td>-</td>
    <td>ElectricalDrive.HighVoltageBattery.StateOfCharge (percent)</td>
    <td>EV_BATTERY_LEVEL (WH), INFO_EV_BATTERY_CAPACITY (WH)</td>
  </tr>
  <tr>
    <td>6. GPS Position & Time at Current Value</td>
    <td>Vehicle.Cabin.Infotainment.Navigation.CurrentLocation.Latitude (degrees), Vehicle.Cabin.Infotainment.Navigation.CurrentLocation.Longitude, Vehicle.Cabin.Infotainment.Navigation.CurrentLocation.Altitude</td>
    <td>VSS has no sensor value for GPS/GNSS time. But depending on implementation GNSS observations may be accompanied with system timestamp</td>
    <td>-</td>
    <td>Position.LastKnown.Latitude, Position.LastKnown.Longitud (WGS84 degrees)</td>
    <td>(Not part of Vehicle HAL)</td>
  </tr>
  <tr>
    <td>7. Service Indicator</td>
    <td>Vehicle.Powertrain.CombustionEngine.OilLifeRemaining (seconds) (?)</td>
    <td>VSS has no explicit service indicator. There is an attribute (!) for remaining oil life which can be considered similar to time-based datapoints used for OEMs. 
        But there might be several factors specifying time to service, not only status of engine oil, e.g. air filters, compartment filters, drive belts, transmission oil.
        Suggestion: Refactor service indicators in VSS. Proposal: Two datapoints, one based on distance, one based on time. Negative value means overdue service.
    </td>
    <td>kmToService (km), monthsToService (months, integer), serviceWarningStatus (NORMAL, ALMOST_TIME_FOR_SERVICE, TIME_FOR_SERVICE, TIME_EXCEEDED), serviceWarningTrigger (CALENDAR_TIME, DISTANCE, ENGINE_HOURS, ECM)</td>
    <td>Service.Interval.Distance (Residual distance to service, km), Service.Interval.Time (Residual time to service, days)</td>
    <td>-</td>
  </tr>
</table>
