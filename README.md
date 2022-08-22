# ITFINDEN 2022 HTML-Email-Notifications-Templates-for-Nagios

Nagios Configuration
For the host and services notification alerts, add these lines to your Nagios commands file (usually located in the Nagios configurations directory and named 'objects') as command definitions:
# 'notify-host-by-email-html' command definition
define command {
	command_name	notify-host-by-email-html
	command_line    $USER1$/php-html-email/nagios_host_mail "$NOTIFICATIONTYPE$" "$HOSTNAME$" "$HOSTALIAS$" "$HOSTSTATE$" "$HOSTADDRESS$" "$HOSTOUTPUT$" "$SHORTDATETIME$" "$CONTACTEMAIL$" "$TOTALHOSTSUP$" "$TOTALHOSTSDOWN$" "$NOTIFICATIONAUTHOR$" "$NOTIFICATIONCOMMENT$" "$LONGDATETIME$" "$HOSTDURATION$" "$HOSTDURATIONSEC$" "$LASTHOSTCHECK$" "$LASTHOSTSTATECHANGE$" "$NOTIFICATIONISESCALATED$" "$HOSTATTEMPT$" "$MAXHOSTATTEMPTS$" "$NOTIFICATIONRECIPIENTS$"
}

# 'notify-service-by-email-html' command definition
define command {
	command_name	notify-service-by-email-html
	command_line	$USER1$/php-html-email/nagios_service_mail "$NOTIFICATIONTYPE$" "$HOSTNAME$" "$HOSTALIAS$" "$HOSTSTATE$" "$HOSTADDRESS$" "$SERVICEOUTPUT$" "$SHORTDATETIME$" "$SERVICEDESC$" "$SERVICESTATE$" "$CONTACTEMAIL$" "$SERVICEDURATIONSEC$" "$SERVICEEXECUTIONTIME$" "$TOTALSERVICESWARNING$" "$TOTALSERVICESCRITICAL$" "$TOTALSERVICESUNKNOWN$" "$LASTSERVICEOK$" "$LASTSERVICEWARNING$" "$SERVICENOTIFICATIONNUMBER$" "$LONGSERVICEOUTPUT$" "$NOTIFICATIONAUTHOR$" "$NOTIFICATIONCOMMENT$" "$SERVICEDURATION$" "$NOTIFICATIONISESCALATED$" "$SERVICEATTEMPT$" "$MAXSERVICEATTEMPTS$" "$NOTIFICATIONRECIPIENTS$"
}
Now that the command object has been configured, you must tell your contacts to use this new command. I have a generic-contact template that all of my individual contacts inherit from, thus I only have to update the template to use the new command, like seen here below:
define contact{
	name	generic-contact
	register	0
	service_notification_commands	notify-service-by-email-html
	host_notification_commands	notify-host-by-email-html
Restart Nagios to pick up the changes.
PHPMailer Configuration
Open up these files and and scroll to the bottom to find the default configuration using PHPMailer. Say, to make it send email to your Gmail via Google SMTP server, just follow the configuration as stated.

<repo>/php-html-email/nagios_host_mail
<repo>/php-html-email/nagios_service_mail
Using Gmail SMTP
$mail = new PHPMailer;
#$mail->SMTPDebug = 3;
$mail->isSMTP();
$mail->SMTPAuth = true;
$mail->SMTPSecure = 'tls';
$mail->Host = 'smtp.gmail.com';
$mail->Port = 587;
$mail->Username = 'someone@example.com';
$mail->Password = 'somepassword';
