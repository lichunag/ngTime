# ngTime
获取验证码，倒计时
<!DOCTYPE html>
<html lang="en" ng-app="indexApp">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="../js/angular.js"></script>
</head>
<body ng-controller="indexCtrl">
    {{date}}
    <script>
        angular.module('indexApp',[])
                .controller('indexCtrl',function($scope,$interval){
                    var h=23,m=59,s=59;
                    $scope.date='24时00分00秒';

                    $interval( function run(){
                        --s;
                        if(s<0){
                            --m;
                            s=59;
                        }
                        if(m<0){
                            --h;
                            m=59;
                        }
                        if(h<0){
                            h=00;
                            s=00;
                            m=00;
                        }
                        $scope.date = h+'时'+m+'分'+s+'秒'
                    },1000);

                })

    </script>
</body>
</html>


<!DOCTYPE html>
<html lang="en" ng-app="indexApp">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="../js/bootstrap.css">
    <script src="../js/angular.js"></script>
</head>
<body ng-controller="indexCtrl">
    <button class="btn btn-default" ng-click="change()"
            ng-disabled="vm.kedian">
        {{vm.data}}
    </button>
    <script>
        angular.module('indexApp',[])
                .controller('indexCtrl',function($scope,$interval){
                    $scope.vm={
                        data:'获取验证码',
                        kedian:false,
                        time:60
                    };

                    $scope.change = function(){
                        $scope.vm.kedian =true;
                        $interval(function(){
                            $scope.vm.data = '重新获取'+$scope.vm.time+'s';
                            $scope.vm.time--;
                            if($scope.vm.time ==0){
                                $scope.vm.kedian =false;
                                $scope.vm.data='重新获取';
                                $scope.vm.time=60;
                            }
                        },1000,$scope.vm.time)
                    }

                })
    </script>
</body>
</html>
