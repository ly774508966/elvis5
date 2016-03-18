elvis5
========

####  html5(webgl) based web-front-end application framework ####



### Usage ###

```html
<script src='three.js'></script>
<script src='core.js'></script>
```
### Example ###
* 전체화면예제
```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>전체화면 예제 </title>
    <meta name="viewport" content="width=device-width, initial-scale=1,maximum-scale=1.0, user-scalable=no">

    <script src='../libs/threejs/three.js'></script>
    <script src="../libs/threejs/js/controls/OrbitControls.js"></script>
    <script src="../libs/ramb3d/core.js"></script>

    <style>

        body {
            margin: 0px; /* 화면 여백 제거   */
            overflow: hidden /* 스크롤바 없애기  */
        }

    </style>

</head>
<body>

<script>

    var Smgr = new  esparty.elvis3d.scene.SceneManager({
        camera : {
            fov : 45,
            far : 5000,
            near : 1,
            position : new THREE.Vector3(0, 5, 10),
            lookat : new THREE.Vector3()

        },
        renderer : {
            type : 'webgl',
            clear : {
                color : 0x000000,
                alpha : 1
            }
        },
        setup : function() {

            //초기화 코드는 여기에서 코딩한다.
            var scope = this;

            //그리드헬퍼
            var helper =  new THREE.GridHelper( 50, 1 );
            helper.setColors(0x00ff00,0xff0000);
            scope.scene.add(helper);

            //오빗컨트롤
            //카메라의 현재 위치 기준으로 시작한다.
            var controls = new THREE.OrbitControls( this.camera ,this.renderer.domElement);
            controls.target.set(0,0,0);
            controls.update();

        },
        event : {
            onWindowResize : function() {
                //동적으로 창의 크기가 바뀌면 이부분이 콜백된다.
                this.updateAll({
                    resize : {
                        width :  window.innerWidth,
                        height : window.innerHeight
                    }
                });
            },
            onUpdate : function(event) {

                this.updateAll();
            },
            onMouseDown : function(event) {

            },
            onMouseMove : function(event) {

                //var mx = ( event.offsetX / this.window_size.width ) * 2 - 1;
                //var my = - ( event.offsetY / this.window_size.height ) * 2 + 1;

            },
            onKeyDown : function(event) {
                //console.log(event);
            }
        }
    });

</script>

</body>
</html>
```


### Change log ###

