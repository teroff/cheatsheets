# pass with OTP

## Read QA code and send the value in the pass 
	zbarimg -q --raw download.png | pass otp insert coinbase

## To read QA code using the webcam
	zbarcam -q --raw | pass otp insert totp-secret

## Generate a 2FA code using this token:
	pass otp totp-secret
