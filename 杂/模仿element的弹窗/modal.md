```javascript
class Common {
	constructor() {
		this.btnColor = {
			primary: 'modal-button-primary',
			error: 'modal-button-error',
			success: 'modal-button-success',
			info: 'modal-button-info',
			warn: 'modal-button-warn',
		}
		this.alertColor = {
			success: 'alert-success',
			info: 'alert-info',
			warn: 'alert-warn',
			error: 'alert-error',
		}
	}
	getElByClassName(className) {
		return document.getElementsByClassName(className);
	}
	createEl(el, className, innerHtml, parentNode) {
		const _el = document.createElement(el);
		if (className) _el.className = className;
		if (innerHtml) _el.innerHTML = innerHtml;
		if (parentNode) parentNode.appendChild(_el);
		return _el;
	}
	createDom(html) {
		document.body.appendChild(html);
	}
}
class Alert extends Common {
	constructor() {
		super()
	}
	alert(config) {
		const alertBox = this.createEl('div', 'alert fadeIn '), 
		defaultHeight = 60, 
		defaultZIndex = 2020,
		defaultTime = 3000,
		that = this;
		
		const count = that.getElByClassName('alert').length - that.getElByClassName('alert-remove').length;
		alertBox.className += that.alertColor[config.type || info];
		alertBox.style.top = (defaultHeight * count) + 'px';
		alertBox.style.zIndex = defaultZIndex + count;
		
		const alertBody = that.createEl('div', 'alert-box', '<i></i><p>'+ config.message +'</p>', alertBox);
		
		setTimeout(() => {
			alertBox.className = 'alert fadeOut alert-remove ' + that.alertColor[config.type || info];
			const alerts = that.getElByClassName('alert');
			const alertsLen = alerts.length;
			if (alertsLen > 0) {
				for (let i = 0; i < alertsLen; i++) {
					alerts[i].style.top = (parseInt(alerts[i].style.top) - defaultHeight) + 'px'
				}
			}
			setTimeout(() => alertBox.remove(), 500)
		}, defaultTime);
		
		that.createDom(alertBox);
	}
}
class Confirm extends Common {
	constructor() {
		super()
	}
	confirm(config) {
		//	简单处理下message不存在问题
		if (typeof config.message !=='string') {
			throw new Error('message值为String类型。')
		}
		if (!config.message.trim()) {
			throw new Error('请给予message参数默认值。')
		}
		const _c = {
			message: config.message,
			title: config.title || '提示',
			shade: config.shade || false,
			shadeClose: config.shadeClose || false,
			headClosebtn: config.headClosebtn || true,
			width: config.width || '35%',
			button: config.button || []
		};
		const that = this, _html = that.createEl('div', 'modal-wrapper');
		if (config.shade) {
			_html.className += ' modal-shadow';
		}
		const confirm = that.createEl('div', 'confirm fadeIn');
		confirm.style.width = _c.width;
		
		const mHead = that.createEl('div', 'confirm-header', '<span class="confirm-title">'+ _c.title +'</span>', confirm);
		if (_c.headClosebtn) {
			const mHeadbtn = that.createEl('button', 'confirm-headbtn', '<i class="confirm-close"></i>', mHead);
			mHeadbtn.type = 'button';
			mHeadbtn.onclick = function() {
				that.destory();
			}
		}
		
		const bodyMsg = that.createEl('div', 'confirm-body', _c.message, confirm);
		
		const mFoot = that.createEl('div', 'confirm-footer', '', confirm);
		const span = that.createEl('span', '', '', mFoot);
		const cancelBtn = that.createEl('span', 'modal-button modal-button-default', '<span>取消</span>', span);
		cancelBtn.onclick = function() {
			that.destory()
		}
		
		const btnLen = _c.button.length;
		if (btnLen > 0) {
			for (let i = 0; i < btnLen; i++) {
				let className = '', title = '';
				className = 'modal-button ' + that.btnColor[_c.button[i].type]
				title = '<span>' + _c.button[i].name + '</span>';
				const btn = that.createEl('button', className, title, span);
				btn.type = 'button';
				btn.onclick = function() {
					_c.button[i].click.call(that);
				}
			}
		}		
						
		_html.appendChild(confirm);
		
		if (config.shade && config.shadeClose) {
			document.onclick = function(e) {
				if (e.target.className.indexOf('modal-wrapper') !== -1) {
					that.destory();
				}
			}
		}
		this.createDom(_html);
	}
	destory() {
		let that = this, modal = null;
		modal = that.getElByClassName('modal-wrapper')[0];
		that.getElByClassName('confirm')[0].className = 'confirm fadeOut';
		modal.className = 'modal-wrapper';
		setTimeout(() => modal.remove(), 500)
	}
}
const _confirm = new Confirm();
const _alert = new Alert();

const Modal = {
	confirm: config => _confirm.confirm.call(_confirm, config),
	alert: config => _alert.alert.call(_alert, config),
}

```
