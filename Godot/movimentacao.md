# Movimentação em Cena 2D
### Obs: Para entender a lógica por trás do código, o trecho "if left_right: ..." obtém valores positivos, ficando à direita em um plano cartesiano. Para podermos ir para a esquerda, utilizamos "else: velocity.x = left_right * -SPEED"
```
extends CharacterBody2D;

const SPEED = 300;
const JUMP_VELOCITY = -400

func _ready():
	anim.play("walk_right")

func _physics_process(_delta):
	var left_right = Input.get_axis('ui_left', 'ui_right');
	var top_down = Input.get_axis('ui_up', 'ui_down');
	if left_right: 
		velocity.x = left_right * SPEED;
	else: 
		velocity.x = left_right * -SPEED
	if top_down:
		velocity.y = top_down * SPEED;
	else:
		velocity.y = top_down * -SPEED
	move_and_slide()
```

# Movimentação em Cena 3D
```
extends CharacterBody3D

const SPEED = 14;
const JUMP_VELOCITY = 25;
const fall_acceleration = 75;

func _physics_process(delta):
	var left_right = Input.get_axis('ui_left', 'ui_right');
	var top_down = Input.get_axis('ui_up', 'ui_down');
	var jump = Input.is_action_just_pressed("ui_accept");
	if left_right: 
		velocity.x = left_right * SPEED;
	else: 
		velocity.x = move_toward(velocity.x, 0, SPEED)
	if top_down:
		velocity.z = top_down * SPEED;
	else:
		velocity.z = move_toward(velocity.y, 0, SPEED)
	if jump and is_on_floor():
		velocity.y += JUMP_VELOCITY - delta
	if not is_on_floor():
		velocity.y -= fall_acceleration * delta
	move_and_slide()
```
