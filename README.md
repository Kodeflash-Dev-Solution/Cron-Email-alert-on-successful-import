# Cron-Email-alert-on-successful-import
```php
function wt_pipe_cron_ended(){

    $email = 'asd@example.org, ert@example.org';
    wp_mail( $email, "Product Auto Import Export", 'Product scheduled import completed.' );

}

add_action('wt_pipe_cron_ended', 'wt_pipe_cron_ended');
```

# Email alert with import log
```php
add_action('rod_scheduled_action_finished', 'rod_scheduled_action_finished', 10,1);
function wt_scheduled_action_finished($out){
  ini_set('max_execution_time', -1);
  ini_set('memory_limit', -1);        
  $wt_log_path = WP_CONTENT_DIR . '/webtoffee_iew_log'; // wp content path - fixed WP violation
  $files = glob("$wt_log_path/*.*");
  $files = array_combine($files, array_map('filectime', $files));
  arsort($files);
  $destination = key($files);
  $email = 'user@mail.com';//Input your email ID
  $object= 'Products imported successfully!';//Specify the subject for email
  $message = 'OK. Automatic import performed SUCCESSFULLY. : ' .date('l d/m/Y H:i:s', time() ). '';//Enter the message
  $mail_attachment = array($destination);   
  $headers = '';
  wp_mail( $email, $object, $message,$headers,$mail_attachment );
}
```
