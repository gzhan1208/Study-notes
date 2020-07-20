```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>Modal</title>
		<link rel="stylesheet" type="text/css" href="modal.css"/>
	</head>
	<body>
		<div class="btn-container">
			<button type="button" class="modal-button modal-button-primary" onclick="modal(0)">Modal</button>
			<button type="button" class="modal-button modal-button-error" onclick="modal(1, 'error')">Alert</button>
			<button type="button" class="modal-button modal-button-success" onclick="modal(1, 'success')">Alert1</button>
			<button type="button" class="modal-button modal-button-info" onclick="modal(1, 'info')">Alert2</button>
			<button type="button" class="modal-button modal-button-warn" onclick="modal(1, 'warn')">Alert3</button>
		</div>
		<script src="modal.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			function modal(type, alertColor) {
				if (type) {
					Modal.alert({
						message: '这是一条测试信息！',
						type: alertColor,
					})
				} else {
					/* 
					 title: String 选填，标题。默认为标题
					 message: String 必填，弹窗内容
					 shade: Boolean 选填，是否开启遮罩层。默认为false
					 shadeClose: Boolean 选填，shade为true时可用，点击遮罩层是否关闭弹窗。默认为false
					 width: String 选填，默认值为35%
					 button: Object 选填，默认只给关闭弹窗的取消按钮。可以自定义添加按钮: name（按钮名称）、type（按钮颜色类型）、click（按钮点击事件，调用destory时关闭窗口）
					 */
					Modal.confirm({
						title: '',
						message: '<span style="color: red">测试</span>',
						shade: true,
						shadeClose: true,
						// width: '420px',
						button: [
							{
								name: 'primary',
								type: 'primary',
								click: function() {
									console.log('点击了再确定');
									this.destory()
								}
							},
							{
								name: 'error',
								type: 'error',
								click: function() {
									console.log('点击了确定');
									Modal.alert({
										message: '这是弹窗内的一条测试信息！',
										type: 'error',
									})
								}
							},
							{
								name: 'warn',
								type: 'warn',
								click: function() {
									console.log('点击了再确定1');
									Modal.alert({
										message: '这是弹窗内的一条测试信息！',
										type: 'warn',
									})
								}
							},
							{
								name: 'info',
								type: 'info',
								click: function() {
									console.log('点击了再确定2');
									Modal.alert({
										message: '这是弹窗内的一条测试信息！',
										type: 'info',
									})
								}
							},
							{
								name: 'success',
								type: 'success',
								click: function() {
									console.log('点击了再确定3');
									Modal.alert({
										message: '这是弹窗内的一条测试信息！',
										type: 'success',
									})
								}
							}
						]
					})
				}
			}
		</script>
	</body>
</html>

```
