<script>
    import "../assets/icon-moon.svg";
</script>

<header>
    <h1>devfinder</h1>
    <button  class="right-header">
        <h3 class="dark">DARK</h3>
        <img class="icon-moon" alt="moon img">
    </button>
</header>

<style>
    header {
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-top: 31px;
    }

    h1 {
        color: #222731;
        font-size: 26px;
        font-weight: 700;
        line-height: 39px;
    }
    .right-header {
        display: flex;
        padding-left: 0.125rem;
        justify-content: center;
        align-items: flex-start;
        gap: 1rem;
        background: #F6F8FF;
        border:none;
    
       
    }

    .dark {
        color: #4B6A9B;
        font-size: 13px;
        font-weight: 700;
        letter-spacing: 2.50px;
        line-height: 19px;
    }

    .icon-moon {
        content: url(../assets/icon-moon.svg);
    }
    @media screen and (min-width: 38rem){
       header{
        margin-top: 8.75rem;

       }
  
    }
    
    @media screen and (min-width: 900px){
        header{
        margin-top: 9rem;
    }
    /* .icon-sun {
        content: url(../assets/icon-sun.svg);
    } */
    }
   
</style>