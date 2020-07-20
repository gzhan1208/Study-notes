```javascript
.btn-container {
	display: flex;
	flex-direction: column;
	justify-content: center;
	width: 80px;
	margin: 15vh 0 0 15vw;
}
.btn-container button {
	margin-bottom: 15px;
}

.modal-wrapper {
	position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    overflow: auto;
    margin: 0;
}
.modal-shadow {
	background-color: rgba(0, 0, 0, 0.3);
}
/* confirm */
.confirm {
	position: relative;
    margin: 0 auto 50px;
    background: #fff;
    border-radius: 2px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, .3);
    box-sizing: border-box;
    width: 35%;
    margin-top: 15vh;
}
.confirm-header {
	padding: 20px 20px 10px;
}
.confirm-title {
	line-height: 24px;
    font-size: 18px;
    color: #303133;
}
.confirm-headbtn {
	position: absolute;
    top: 20px;
    right: 20px;
    padding: 0;
    background: transparent;
    border: none;
    outline: none;
    cursor: pointer;
    font-size: 16px;
}
.confirm-headbtn .confirm-close {
	width: 20px;
	height: 20px;
	margin: auto;
	position: relative;
    font-style: normal;
    font-weight: 400;
    font-variant: normal;
    text-transform: none;
    line-height: 1;
    vertical-align: baseline;
    display: inline-block;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
.confirm-close::before,
.confirm-close::after {
  content: "";
  position: absolute;
  height: 16px;
  width: 1px;
  top: 2px;
  right: 9px;
  background: #909399;
}
.confirm-headbtn .confirm-close:hover::before,
.confirm-headbtn .confirm-close:hover::after {
	background: #409eff;
}
.confirm-close::before {
  transform: rotate(45deg);
}
.confirm-close::after {
  transform: rotate(-45deg);
}
.confirm-body {
	padding: 30px 20px;
	color: #606266;
	font-size: 14px;
	word-break: break-all;
}
.confirm-footer {
	padding: 10px 20px 20px;
    text-align: right;
    box-sizing: border-box;
}
.confirm-footer .modal-button+.modal-button {
	margin-left: 10px;
}
/* alert */
.alert {
	position: fixed; 
	left: 50%; 
	top: -50px; 
	margin-left: -175px;
	background: #edf2fc;
	border: 1px solid #ebeef5;
	border-radius: 10px; 
	min-width: 350px;
	transition: opacity .3s,transform .4s,top .4s;
	z-index: 99
}
.alert-box {
	position: relative;
	width: 100%;
	height: 100%
}
.alert-box p {
	margin: 0;
	font-size: 14px;
	padding: 14px 15px 15px 20px;
}
.alert-error {
	background-color: #fef0f0;
    border-color: #fde2e2;
	color: #f56c6c;
}
.alert-success {
	background-color: #f0f9eb;
    border-color: #e1f3d8;
	color: #67c23a;
}
.alert-info {
	color: #909399;
}
.alert-warn {
	background-color: #fdf6ec;
    border-color: #faecd8;
	color: #e6a23c;
}

/* button */
.modal-button {
	display: inline-block;
    line-height: 1;
    white-space: nowrap;
    cursor: pointer;
    background: #fff;
    border: 1px solid #dcdfe6;
    color: #606266;
    -webkit-appearance: none;
    text-align: center;
    box-sizing: border-box;
    outline: none;
    margin: 0;
    transition: .1s;
    font-weight: 500;
    -moz-user-select: none;
    -webkit-user-select: none;
    -ms-user-select: none;
    padding: 12px 20px;
    font-size: 14px;
    border-radius: 4px;
}
.modal-button-primary {
	color: #fff;
    background-color: #409eff;
    border-color: #409eff;
}
.modal-button-error {
	color: #fff;
	background-color: #f56c6c;
    border-color: #f56c6c;
}
.modal-button-success {
	color: #fff;
	background-color: #67c23a;
    border-color: #67c23a;
}
.modal-button-info {
	color: #fff;
	background-color: #909399;
    border-color: #909399;
}
.modal-button-warn {
	color: #fff;
	background-color:#e6a23c;
    border-color: #e6a23c;
}
.modal-button:focus, .modal-button:hover {
    color: #409eff;
    border-color: #c6e2ff;
    background-color: #ecf5ff;
}
.modal-button-primary:focus, .modal-button-primary:hover {
	color: #fff;
    background: #66b1ff;
    border-color: #66b1ff;
}
.modal-button-error:focus, .modal-button-error:hover {
	color: #fff;
    background: #f78989;
    border-color: #f78989;
}
.modal-button-success:focus, .modal-button-success:hover {
	color: #fff;
    background: #85ce61;
    border-color: #85ce61;
}
.modal-button-info:focus, .modal-button-info:hover {
	color: #fff;
    background: #a6a9ad;
    border-color: #a6a9ad;
}
.modal-button-warn:focus, .modal-button-warn:hover {
	color: #fff;
    background: #ebb563;
    border-color: #ebb563;
}


/* animation */
@-webkit-keyframes fadeIn {
    0% {
		opacity: 0;
		-webkit-transform: translateY(0);
	}
    100% {
		opacity: 1;
		-webkit-transform: translateY(20px);
	}
}
@keyframes fadeIn {
    0% {
	   opacity: 0;
	   transform: translateY(0);
	}
    100% {
	   opacity: 1;
	   transform: translateY(20px);
	}
}
.fadeIn {
    -webkit-animation-name: fadeIn;
    animation-name: fadeIn;
}
@-webkit-keyframes fadeOut {
    0% {
	   opacity: 1;
	   -webkit-transform: translateY(20px);
	}
    100% {
		opacity: 0;
		-webkit-transform: translateY(0);
	}
}
@keyframes fadeOut {
   0% {
	   opacity: 1;
	   transform: translateY(20px);
   }
   100% {
	   opacity: 0;
	   transform: translateY(0);
   }
}
.fadeIn, .fadeOut {
	-webkit-animation-duration: .6s;
	animation-duration: .6s;
	-webkit-animation-fill-mode: both;
	animation-fill-mode: both;
}
.fadeOut {
    -webkit-animation-name: fadeOut;
    animation-name: fadeOut;
}
```
