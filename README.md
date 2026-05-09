<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Social App</title>
<meta name="google-adsense-account" content="ca-pub-5968278007440676">
     <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-5968278007440676"
     crossorigin="anonymous"></script>
<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial;
}

body{
    background:#111;
    color:white;
}

/* NAVBAR */

.navbar{
    background:#000;
    padding:15px;
    display:flex;
    justify-content:space-between;
    align-items:center;
}

.logo{
    color:#00bfff;
    font-size:24px;
    font-weight:bold;
}

.menu a{
    color:white;
    text-decoration:none;
    margin-left:15px;
    cursor:pointer;
}

/* LOGIN */

#loginPage{
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
}

.login-box{
    width:320px;
    background:#222;
    padding:25px;
    border-radius:15px;
    text-align:center;
}

input, textarea{
    width:100%;
    padding:12px;
    margin-top:10px;
    border:none;
    border-radius:10px;
    outline:none;
}

button{
    width:100%;
    padding:12px;
    margin-top:10px;
    border:none;
    border-radius:10px;
    background:#00bfff;
    color:white;
    font-size:16px;
    cursor:pointer;
}

#msg{
    margin-top:10px;
    color:red;
}

/* APP */

#app{
    display:none;
}

/* PAGES */

.page{
    display:none;
}

.active{
    display:block;
}

/* FEED */

.post-box{
    width:90%;
    max-width:500px;
    margin:20px auto;
    background:#222;
    padding:15px;
    border-radius:15px;
}

.post{
    width:90%;
    max-width:500px;
    margin:15px auto;
    background:#222;
    padding:15px;
    border-radius:15px;
}

.username{
    color:#00bfff;
    font-weight:bold;
}

.like-btn{
    background:#ff0055;
}

/* INFO PAGE */

.section{
    width:90%;
    max-width:700px;
    margin:30px auto;
    background:#222;
    padding:20px;
    border-radius:15px;
}

.section h2{
    margin-bottom:15px;
    color:#00bfff;
}

.section p{
    margin-top:10px;
    line-height:1.7;
}

/* FOOTER */

.footer{
    background:#000;
    padding:20px;
    text-align:center;
    margin-top:30px;
}

</style>
</head>

<body>

<!-- LOGIN -->

<div id="loginPage">

    <div class="login-box">

        <h2>tikmess Login</h2>

        <input type="text"
        id="user"
        placeholder="Enter Username">

        <button onclick="login()">
            Login
        </button>

        <div id="msg"></div>

    </div>

</div>

<!-- APP -->

<div id="app">

    <!-- NAVBAR -->

    <div class="navbar">

        <div class="logo">
            tikmess
        </div>

        <div class="menu">

            <a onclick="showPage('homePage')">
                Home
            </a>

            <a onclick="showPage('aboutPage')">
                About
            </a>

            <a onclick="showPage('privacyPage')">
                Privacy
            </a>

        </div>

    </div>

    <!-- HOME PAGE -->

    <div class="page active" id="homePage">

        <!-- CREATE POST -->

        <div class="post-box">

            <textarea
            id="postText"
            rows="4"
            placeholder="Write post..."></textarea>

            <button onclick="addPost()">
                Post
            </button>

        </div>

        <!-- FEED -->

        <div id="feed"></div>

    </div>

    <!-- ABOUT PAGE -->

    <div class="page" id="aboutPage">

        <div class="section">

            <h2>About Us</h2>

            <p>
                Welcome to tikmess.
                Users can create posts,
                like content and interact
                with friends online.
            </p>

            <p>
                Our mission is to provide
                a simple and secure comment
                media platform.
            </p>

        </div>

    </div>

    <!-- PRIVACY PAGE -->

    <div class="page" id="privacyPage">

        <div class="section">

            <h2>Privacy Policy</h2>

            <p>
                We respect your privacy
                and protect your information.
            </p>

            <p>
                Your data is stored safely
                for demo purposes only.
            </p>

            <p>
                We do not share user data
                with third parties.
            </p>

        </div>

    </div>

    <!-- FOOTER -->

    <div class="footer">

        © 2026 tikmess App

    </div>

</div>

<script>

let currentUser = "";

// LOGIN
function login(){

    let user =
    document.getElementById("user").value;

    let msg =
    document.getElementById("msg");

    if(user == ""){

        msg.innerHTML =
        "Enter username";

        return;
    }

    currentUser = user;

    document.getElementById("loginPage")
    .style.display = "none";

    document.getElementById("app")
    .style.display = "block";

    loadPosts();

}

// SHOW PAGE
function showPage(pageId){

    let pages =
    document.querySelectorAll(".page");

    pages.forEach(function(page){

        page.classList.remove("active");

    });

    document.getElementById(pageId)
    .classList.add("active");

}

// ADD POST
function addPost(){

    let text =
    document.getElementById("postText").value;

    if(text == "") return;

    let posts =
    JSON.parse(localStorage.getItem("posts") || "[]");

    posts.unshift({

        user: currentUser,
        text: text,
        likes: 0,
        likedUsers: []

    });

    localStorage.setItem(
        "posts",
        JSON.stringify(posts)
    );

    document.getElementById("postText").value = "";

    loadPosts();

}

// LOAD POSTS
function loadPosts(){

    let posts =
    JSON.parse(localStorage.getItem("posts") || "[]");

    let feed =
    document.getElementById("feed");

    feed.innerHTML = "";

    posts.forEach(function(post,index){

        let liked =
        post.likedUsers.includes(currentUser);

        feed.innerHTML += `

        <div class="post">

            <div class="username">
                ${post.user}
            </div>

            <p style="margin-top:10px;">
                ${post.text}
            </p>

            <button
            class="like-btn"
            onclick="toggleLike(${index})">

            ${liked ? "❤" : "❤️ Like"}

            (${post.likes})

            </button>

        </div>

        `;

    });

}

// LIKE + UNLIKE
function toggleLike(index){

    let posts =
    JSON.parse(localStorage.getItem("posts") || "[]");

    let liked =
    posts[index].likedUsers.includes(currentUser);

    if(liked){

        // UNLIKE
        posts[index].likes--;

        posts[index].likedUsers =
        posts[index].likedUsers.filter(
            user => user != currentUser
        );

    }else{

        // LIKE
        posts[index].likes++;

        posts[index].likedUsers.push(currentUser);

    }

    localStorage.setItem(
        "posts",
        JSON.stringify(posts)
    );

    loadPosts();

}

</script>

</body>
</html>
