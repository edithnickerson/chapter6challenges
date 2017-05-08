
   Chapter Challenges
 +
 +1. Reload the forecast - `ionRefresh`
 +2. Implement the loading component - Like a previous chapter
 +3. Allow reordering of locations - `ionList` reordering
 +4. Use tabs instead of scrolling - Avoid making each tab a new state
 +5. Set Default view - set to primary location once loocations are stored
 +6. Persistence - Since this will be covered in -
 
 Updating the Weather View Controller to use SunCalculator
 +
 +```javascript
 +  $scope.showModal = function () {
 +    if ($scope.modal) {
 +      $scope.modal.show();
 +    } else {
 +      $ionicModal.fromTemplateUrl('views/weather/modal-chart.html', {
 +        scope: $scope
 +      }).then(function (modal) {
 +        $scope.modal = modal;
 +        var days = [];
 +        var day = Date.now();
 +        for (var i = 0; i < 365; i++) {
 +          day += 1000 * 60 * 60 * 24;
 +          days.push(SunCalc.getTimes(day, $scope.params.lat, $scope.params.lng));
 +        }
 +        $scope.chart = days;
 +        $scope.modal.show();
 +      });
 +    }
 +  };
 +  
 


### Updating the Weather Vew Modal Chart Template to use Collection Repeat
 +```
 <ion-modal-view>
 +  <ion-header-bar class="bar-dark">
 +    <h1 class="title">Sunrise, Sunset Chart</h1>
 +    <button class="button button-clear" ng-click="hideModal()">Close</button>
 +  </ion-header-bar>
 +  <ion-content>
 +    <div class="list">
 +      <div class="item" collection-repeat="day in chart">
 +        {{day.sunrise | date:'MMM d'}}: {{day.sunrise | date:'shortTime'}}, {{day.sunset | date:'shortTime'}}
 +      </div>
 +    </div>
 +  </ion-content>
 +</ion-modal-view>


