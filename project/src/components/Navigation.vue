<template>
    <div>
        <nav :class="{'onScroll' : !view.pageOffSet}">
            <div class="headerLogo">
                <h1 class="title">Pagination</h1>
            </div>
            <div class="headerLinks">
                <ul>
                    <li><router-link to="/">Home</router-link></li>
                     <li><router-link to="/about">About</router-link></li>
                </ul>
            </div>
        </nav>
    </div>
</template>
<script>
export default {
    name:"Navigation",
    data() {
        return {
            view:{
                pageOffSet:true,
            }
        }
    },
    created() {
        window.addEventListener("scroll",this.handleScroll)
    },
    methods: {
        handleScroll() {
            if(window.pageYOffset > 0) {
                if(this.view.pageOffSet) {
                    this.view.pageOffSet = false;
                }
            } else {
                  if(!this.view.pageOffSet) {
                    this.view.pageOffSet = true;
                }
            }
        }
    },
}
</script>
<style scoped>
nav {
    display:flex;
    justify-content: space-between;
    padding:10px;
    width:100%;
    position:fixed;
    top:0;
    height:10vh;
    align-items:center;
    background:#eee;
}
nav ul {
    list-style:none;
    margin:10px;
    display: inline-flex;
}
nav ul li {
    margin:10px;
}
nav ul li a {
    text-decoration: none;
    color:#000;
}
.onScroll {
    background:#ff0000;
    color:#fff;
}
.onScroll a {
    color:#fff;
}
</style>