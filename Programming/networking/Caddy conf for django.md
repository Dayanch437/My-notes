
~~~ruby
dayanch03.me {
    encode gzip

    handle_path /static/* {
        root * /srv/my_cv/static
        file_server
    }

    handle_path /media/* {
        root * /srv/my_cv/media
        file_server
    }

    handle {
        reverse_proxy unix//srv/my_cv/my_cv.sock
    }
}

~~~


