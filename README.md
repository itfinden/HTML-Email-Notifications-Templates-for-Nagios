# HTML-Email-Notifications-Templates-for-Nagios
para dejar bonitos los reportes de nagios


/*******************************************************************************

--------------------------------------------------------------------------------

Requirements:

 1. Copy the php-html-email folder to the Nagios plugins directory and make sure all files are owned by the nagios user and also that they are executable!
 2. For the host and services notification alerts, please add these lines to your Nagios commands list:

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

 3. Add the command names to your contact notifications settings, like seen below:
    service_notification_commands	notify-service-by-email-html
    host_notification_commands	notify-host-by-email-html

*******************************************************************************/
