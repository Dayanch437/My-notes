**Force reset your code to match GitHub exactly:**  
(This will overwrite your local files with the pushed code.)

~~~bash
git fetch origin
git reset --hard origin/main
~~~
- Replace `main` with your branch name if different (maybe `master` or another branch).
    
- `fetch` updates your info.
    
- `reset --hard` makes local code **exactly like GitHub**.
    

✅ All your deleted migrations will come back
