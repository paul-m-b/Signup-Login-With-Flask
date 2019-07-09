from flask import Flask, render_template
from flask import Flask, request, redirect
import json
app = Flask(__name__)
users = json.load(open("users.txt"))
@app.route("/")
def run():
    return render_template("index.html")
    

@app.route("/signup", methods=["POST", "GET"])
def signup():
    email = request.form['email']
    passw = request.form['passw']

    if(len(str(email)) == 0 or len(str(passw)) == 0):
        return render_template("signupfailed.html")

    elif (email not in users):
        users[email] = passw
        json.dump(users, open("users.txt", 'w'))
        print (users)
        return render_template("signupsuccess.html")


    else:
        return render_template("signupfailed.html")
    return redirect('/')

@app.route("/login", methods=["POST", "GET"])
def login():
    logemail = request.form['logemail']
    logpassw = request.form['logpassw']

    if (logemail == "admin" and users['admin'] == logpassw):
        return render_template("adminportal.html", logs = users)
    if (logemail in users):
        if (users[logemail] == logpassw):
            return render_template("login.html", logemail=logemail)
        else:
            return render_template("loginfailed.html")
    else:
        return render_template("loginfailed.html")
    
    return redirect('/')
    
@app.route("/changepass", methods=["POST", "GET"])
def changepass():
    username = request.form['username']
    oldpass = request.form['oldpass']
    newpass = request.form['newpass']

    if (users[username] == oldpass):
        users[username] = newpass
        json.dump(users, open("users.txt", 'w'))
        return redirect('/')
    return redirect('/')
     
@app.route("/changeusername", methods=["POST", "GET"])
def changename():
    username = request.form['username']
    password = request.form['password']
    newusername = request.form['newusername']

    if (newusername in users):
        print("Failed changing username, already exists")
        return render_template("signupfailed.html")

    if (users[username] == password):
        users[newusername] = users.pop(username)
        json.dump(users, open("users.txt", 'w'))
        return redirect('/')
    return redirect('/')
 


if (__name__ == "__main__"):
    app.run()
