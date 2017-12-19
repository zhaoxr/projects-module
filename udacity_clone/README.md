
前端纳米学位街机游戏克隆项目
===============================

学生应该用这个[评审标准](https://review.udacity.com/#!/rubrics/499/view))来自我检查自己提交的代码。 确认自己写的函数要是**面向对象的** -  要么是类函数（就像函数 Player 和 Enemy）要么是类的原型链上的函数比如 Enemy.prototype.checkCollisions ， 在类函数里面或者类的原型链函数里面适当的使用关键词 'this' 来引用调用该函数的对象实例。最后保证你的**readme.md**文件要写明关于如何运行和如何玩你的街机游戏的指引。

关于如何开始这个项目的更详细的指导，可以查阅这份[指南](https://gdgdocs.org/document/d/1v01aScPjSWCCWQLIpFqvg3-vXLH2e8_SZQKC8jNO0Dc/pub?embedded=true)。


玩家和敌人显示在画面上
-----------

1、根据提示先把玩家实例化，然后让玩家和敌人显示在画面上

```
	var allEnemies = [];
	var player = new Player(-101,-83);
	Player.prototype.update = function(dt) {};
	Player.prototype.render = function(dt) {};
	Player.prototype.update = function() {
		ctx.drawImage(Resources.get(this.sprite), this.x, this.y);
	};
```
2、让玩家和敌人都动起来

> 敌人动画（通过for循环和随机数来显示多个不同位置移动的敌人）

```
	for(var i = 0; i < 4; i++) {
		var count = 0;
		allEnemies.push(new Enemy(0, (Math.random() * 300 + 100) * i, 500));
		
	}
```
##### 玩家动画（通过handleInput函数来操作玩家的位置）

```
	Player.prototype.handleInput = function(movement) {}
```


##### 碰撞
>	释放checkCollisions（）方法的调用
>	通过checkCollisions()方法来检测玩家的位置和敌人的位置距离范围来判断碰撞---在这里我是判断碰撞三次以后重置玩家和敌人的位置

```	
	function checkCollisions() {
		var count = 0;
 		allEnemies.forEach(function(enemy) {
			if(enemy.x < player.x + 55 && enemy.x + 55 > player.x && enemy.y < player.y + 55 && enemy.y + 55 > player.y) {
				count++;
				if(count > 1) {
					player.reset();
					allEnemies = [];
				}
			}
		});
	}
```
	

##### 成功
>	当玩家的位置移动到水里的时候表示玩家胜利，显示成功图片

```	
	Player.prototype.win = function(){
		var winIcon = document.getElementById('win');
		winIcon.style.display = "block";
		player.reset();
		allEnemies = [];
	}
```

##### 其他

> 在页面中增加开始按钮，当点击按钮的时候，游戏开始

```	
	 state.onclick = function(){}
	 Enemy.prototype.reset = function() {
	 	this.x = Math.random() * 50;
		this.y = Math.random() * 150;
		this.speed = Math.random() * 100;
	 }	/*敌人重置*/
	 Player.prototype.reset = function() {
	 	this.x = -101;
		this.y = -83;
		window.clearInterval(timer);
	 }	/**玩家重置 */
```	