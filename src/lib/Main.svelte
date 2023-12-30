<script lang="ts">
    
  type UserData = {
  login: string;
  avatar_url: string;
  location: string;
  email: string;
  bio: string;
  blog: string;
  twitter_username: string;
  public_repos: number;
  followers: number;
  following: number;
  name:string;
  company:string;
  created_at?: string;
};

  let username:string;
  let error: string | null = null;
  let userData: UserData | null = null;
  let date: Date;

  async function searchUser() {
    try {
      const response = await fetch(`https://api.github.com/users/${username}`);
    
      if (!response.ok) {
              userData = null;
              error = 'No results';
          } else{
      const user = await response.json();
      userData = {
        login: user.login,
        name:user.name,
        avatar_url: user.avatar_url,
        location: user.location,
        email: user.email,
        bio: user.bio,
        twitter_username: user.twitter_username,
        public_repos: user.public_repos,
        followers: user.followers,
        following: user.following,
        company: user.company,
        blog:user.blog,
        created_at: user.created_at,
      };

      if (userData && userData.created_at) {
      date = new Date(userData.created_at);
          }
      error = null;
      }
      
      

    } 
    catch (error) {
      userData = null;
      error = `Something went wrong:`;
      }
     
    }
    function checkInfo(object: string | null, errorText = "Not Available") {
        if (object !== null && object !== undefined) {
            return `${object}`;
        } else {
            return `${errorText}`;
        }
    };


</script>

<main> 
  <label class="search-container">
      <img class="search-icon" alt="search icon">
      <input bind:value={username} type="text" id="user-search" name="user-search" placeholder="Search GitHub username…" />
      {#if error}
      <p class="error-message">{error}</p>
  {/if}
  <button class="button" on:click={searchUser}>Search</button>
  </label>

 <form class="form">
  {#if userData}
      <div class="username">
          <img class="user-logo" alt="user logo" src={userData.avatar_url}> 

            <span class="main-info">
              <p class="name">{userData.name}</p>
              <p class="email">@{userData.login}</p>
              <p class="date"> Joined 
                {`${date.getDate()} ${date.toLocaleString("en-us", {
                  month: "short",
                })} ${date.getFullYear()}`}
            </p>
            </span>
        </div>
         
      
      <div class="user-data">
        <p class="text">{userData.bio}</p>
        <section class="content">
          <span class="repos">
              <p class="info">Repos</p>
              <p class="number">{userData.public_repos}</p>
          </span>
          <span class="followers">
              <p class="info">Followers</p>
              <p class="number">{userData.followers}</p>
          </span>
          <span class="following">
              <p class="info">Following</p>
              <p class="number">{userData.following}</p>
          </span>
      </section>
      <section class="contacts">
      
          <span class = "location">
              <img class ="icon-location" alt="location img" src="/src/assets/icon-location.svg"> 
              <h3 class = "contacts-info"> {checkInfo(userData.location)}</h3>
            
          </span>
          <span class = "github-link">
              <img class ="icon-link" alt="link img" src="/src/assets/icon-website.svg">
               <a href={userData.blog}><h3 class = "contacts-info">{checkInfo(userData.blog)}</h3></a>
          </span>
          <span class = "twitter">
              <img class ="icon-twitter" alt="twitter img" src="/src/assets/icon-twitter.svg">
              <h3 class = "contacts-info">{checkInfo(userData.twitter_username)}</h3>
          </span>
          <span class = "company">
              <img class ="icon-company" alt="company img" src="/src/assets/icon-company.svg">
              <h3 class = "contacts-info">{checkInfo(userData.company)}</h3>
          </span>
      </section>
    </div>
      {:else if error}
      <p>{error}</p>
    {/if}
  
 </form>
</main>


<style>
    
  .search-container{
      padding: 0.41rem 0.44rem 0.47rem 1rem;
      margin-top: 2.25rem;
      display: flex;
      align-items: center;
      border-radius: 0.9375rem;
      background: #FEFEFE;
      box-shadow: 0px 16px 30px -10px rgba(70, 96, 187, 0.20);
  }

  #user-search{
      width: 100%;
      color: #4B6A9B;
      font-size: 0.8125rem;
      font-style: normal;
      font-weight: 400;
      line-height: 1.5625rem; /* 192.308% */
      margin-left: 0.56rem;
      border: none;
      outline: none;
  }
  .user-logo{
      width: 4.375rem;
      height: 4.375rem;;
      border-radius: 4.375rem;
  }
  .search-icon{
      content: url(../assets/icon-search.svg);
  }
  .button{
      border-radius: 0.625rem;
      background: #0079FF;
      padding:0.78rem 1.12rem;
      color: #FFF;
      text-align: center;
      font-size: 0.875rem;
      font-weight: 700;
      margin-left: 0.44rem;
      border: none;
  }
 
  .form{
      margin-top: 1rem;
      padding: 2rem 1.5rem 3rem 1.5rem;
      border-radius: 0.9375rem;
      background: #FEFEFE;
      box-shadow: 0px 16px 30px -10px rgba(70, 96, 187, 0.20);
  }
  .main-info{
      margin-right: 4.38rem;
      margin-left: 1.2rem;
  }
  .username{
      display: flex;
  }
  .name{
      color: #2B3442;
      font-size: 1rem;
      font-weight: 700;
  }
  .email{
      color: #0079FF;
      font-size: 0.8125rem;
      font-weight: 400;
  }
  .date{
      color: #697C9A;
      font-size: 0.8125rem;
      font-weight: 400;
  }
  .text{
      margin-top: 2.12rem;
      color: #4B6A9B;
      font-size: 0.8125rem;
      font-weight: 400;
      line-height: 1.5625rem; 
  }

  .content{
      border-radius: 0.625rem;
      background: #F6F8FF;
      margin-top: 1.44rem;
      padding:1.12rem 0.88rem 1.19rem 0.94rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
  }
  .info{
      color: #4B6A9B;
      text-align: center;
      font-size: 0.6875rem;
      font-weight: 400;
  }
  .number{
      color: #2B3442;
      text-align: center;
      font-size: 1rem;
      font-weight: 700;
      margin-top:0.5rem;
  }
  .contacts{
      margin-top: 1.5rem;
      display: grid;
      grid-template-columns: auto;
      gap: 1rem;
  }
  .contacts-info{
      margin-left:2rem;
      color: #4B6A9B;
      font-size: 0.8125rem;
      font-weight: 400;
      margin-top: -1.5rem;
  }
  .error-message{
      color: #F74646;
      font-size: 0.9375rem;
      font-weight: 700;
      white-space: nowrap; 
      margin-right: 1.5rem;
  }


  @media screen and (min-width: 765px){
      .form{
      margin-top: 1.5rem;
      padding: 2.5rem;
      
  }
      .contacts{
      display: grid;
      grid-template-columns: repeat(2, 1fr);
}
      .content{
      margin-top: 2rem;
      padding:1rem 6rem 1rem 2rem;
  }

  }

  
  
  @media screen and (min-width:1024px){
      .form{
      margin-top: 1.5rem;
      padding: 2.75rem 3rem 3rem 3rem;
      
  }
     .name{
      font-size: 1.625rem;
  }
     .email{
      font-size: 1rem;
  }
    .date{
      font-size: 0.9375rem;
       margin-left: 19rem;
      margin-top: -3.5rem;
    
      text-align: right;
  }
    .text{ 
    font-size: 0.9375rem;
  }
  .number{
      
      font-size:1.375rem;
     
  }
  
  .user-logo{
    width: 7.3125rem;
    height: 7.3125rem;
  }
      .contacts{
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      grid-auto-columns: min-content;
      
    }
      .content{
      margin-top: 2rem;
      padding:1rem 6rem 1rem 2rem;
  }
 
  .main-info{
    margin-left: 2.31rem;

  }
  .user-data{
    margin-top: -4rem;
    margin-left:  9.8rem;
  }

  }

</style>