elvis5
========

####  html5(webgl) based dynamic 3d web-front-end application framework ####

랜더러는 three.js,물리엔진은 cannon.js, 애니메이션은tween.js 사용해서 구성한 프레임웍입니다.


### Example ###
* 전체화면기본예제
```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>전체화면 예제 </title>
    <meta name="viewport" content="width=device-width, initial-scale=1,maximum-scale=1.0, user-scalable=no">

    <script src='../libs/threejs/three.js'></script>
    <script src="../libs/threejs/js/controls/OrbitControls.js"></script>
    <script src="../libs/elvis5/core.js"></script>

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

            //씬노드 추가
            var geometry = new THREE.CubeGeometry(1,1,1);
            var material = new THREE.MeshBasicMaterial(
                    {
                        color: 0x00ff00,
                        wireframe : true

                    }
            );
            var node = new THREE.Mesh(geometry, material);
            node.name = 'wire_cube';
            scope.scene.add(node);

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

* 창모드예제
창모드에 필요한 DOM 선언 
```html

<div id='mycanvas' style="
    margin: auto;
    width: 320px;height: 240px;" ></div>

```

esparty.elvis3d.scene.SceneManager 를 초기화 시킬때 container 에 DOM객체를 넣어준다.

```javascript
var Smgr = new  esparty.elvis3d.scene.SceneManager({
        camera : {
            fov : 45,
            far : 5000,
            near : 1,
            position : new THREE.Vector3(5, 10, 10),
            lookat : new THREE.Vector3()

        },
        renderer : {
            type : 'webgl',
            container : document.querySelector('#mycanvas'),
            clear : {
                color : 0x000000
            }

        },
        ... 이하생략 ...
});
```




### Change log ###

