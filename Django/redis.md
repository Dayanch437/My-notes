y
✅ **Install Redis Server**

~~~bash
sudo apt update
sudo apt install redis-server
~~~


✅ **Enable and Start Redis**

~~~bash
sudo systemctl enable redis
sudo systemctl start redis
~~~


✅ **Check Redis Status**
~~~bash
sudo systemctl status redis
~~~

✅ **Test Redis Connection**
~~~bash
redis-cli ping
~~~
Expected output:
~~~nginx
PONG
~~~

