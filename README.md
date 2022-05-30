# SMTPX

Fork from [mail](https://github.com/farmerx/mail)

## Support Auth

* `LOGIN`: `smtpx.LoginAuth(email.Username, email.Password)`
* `CRAM-MD5`: `smtp.CRAMMD5Auth(email.Username, email.Password)`
* `PLAIN`: `smtp.PlainAuth(email.Identity, email.Username, email.Password, email.Host)`
* `NTLM`: `smtpx.NTLMAuth(email.Host, email.Username, email.Password, mail.NTLMVersion1)`

## Support Secure:

* SSL
* TLS
* NONE

## Usage

```go
email := smtpx.NewEMail(`{"port":25}`) // [587 NTLM AUTH] [465，994]
email.From = `user1@example.com`
email.Host = `smtp.example.com`
email.Username = `user1` // if NTLM: "domain/username"
email.Secure = `` // SSL，TSL
email.Password = `************`
authType := `LOGIN`
switch authType {
case ``:
	email.Auth = nil
case `LOGIN`:
	email.Auth = smtpx.LoginAuth(email.Username, email.Password)
case `CRAM-MD5`:
	email.Auth = smtp.CRAMMD5Auth(email.Username, email.Password)
case `PLAIN`:
	email.Auth = smtp.PlainAuth(email.Identity, email.Username, email.Password, email.Host)
case `NTLM`:
	email.Auth = smtpx.NTLMAuth(email.Host, email.Username, email.Password, NTLMVersion1)
default:
	email.Auth = smtp.PlainAuth(email.Identity, email.Username, email.Password, email.Host)
}

email.To = []string{`user2@example.com`}
email.Subject = `send mail success`
email.Text = "Dear User2:\n\n Hello World!"
email.AttachFile(reportFile)
if err := email.Send(); err != nil {
      fmt.Println(err)
}
```
