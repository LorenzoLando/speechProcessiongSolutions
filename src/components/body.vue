<template>
   <div>
    <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">{{loginText}}</button>
    <div v-if="typeof this.user.userToken !== 'undefined' && this.user.userToken !== ''" >
       <table class="table">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Title</th>
              <th scope="col">length</th>
              <th scope="col">Recording Date</th>
               <th scope="col">More data</th>
               <th scope="col">Download</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(record, index) in records" v-bind:key="index">
              <th scope="row">{{index}}</th>
              <td>{{record.title}}</td>
              <td>{{record.length}}</td>
              <td>{{record.date}}</td>
              <td>
                <input v-on:click="checkRecord(record.uuid)" type="submit"  value="Check more data" class="btn btn-secondary" data-toggle="modal" data-target="#uuidModal">
              </td>
              <td>
                <input  v-on:click="downloadRecord(record.uuid)" type="Delete"  value="Download" class="btn btn-danger" download="record.title.mp3">
              </td>
              <!-- Modal -->
              <div class="modal fade" id="uuidModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
                <div class="modal-dialog" role="document">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h5 class="modal-title" id="exampleModalLabel">Metadata</h5>
                      <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                      </button>
                    </div>
                    <div class="modal-body">
                      <p>UUID: {{record.uuid}}</p>
                      <p>State: {{currentState}}</p>
                    </div>
                    <div class="modal-footer">
                      <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                    </div>
                  </div>
                </div>
              </div>
            </tr>
           </tbody>
        </table>
    </div>
    <!--Login Modal -->
      <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">Log In</h5>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
                <form>
                  <div class="form-group">
                    <label for="exampleInputEmail1">Email address</label>
                    <input v-model="userAutentication.userMail" type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter email">
                    <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
                  </div>
                  <div class="form-group">
                    <label for="exampleInputPassword1">Password</label>
                    <input v-model="userAutentication.password" type="password" class="form-control" id="exampleInputPassword1" placeholder="Password">
                  </div>
            </form>
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
              <button v-on:click="loginUser" type="button" class="btn btn-primary" data-dismiss="modal">Login</button>
            </div>
          </div>
        </div>
      </div>
    <!--/ Login Modal -->
  </div>
</template>
<script>
export default {
  data () {
    return {
      loginText: "Log In!",
      userAutentication:{
        userMail: "",
        password: ""
      },
      user: {
        userName: "",
        userToken: ""
      },
      records: [],
      currentUUID: '',
      currentState: ''
    }
  },
  mounted: function() {
  console.log('****************************************');
  console.log('body component mounted');
  console.log('****************************************');
  },
  methods: {
    downloadRecord: function(uuid) {
        console.log(uuid);
        console.log(`Bearer ${this.user.userToken}`);
       const options = {
          method: 'GET',
          headers: {
            "Content-Type": "application/json",
            "accept": "application/json",
            'Authorization': `Bearer ${this.user.userToken}`,
            'uuid': uuid
          }
        };
        fetch(`https://voicedrive.speakachu.com/voice-memos/${uuid}/download`, options)
        .then((response) => {
           return response
           
         
        })
        .then((data) => {
            console.log(data.headers);
        });
        
    },
    checkRecord: function(uuid){
     
         const options = {
          method: 'GET',
          headers: {
            "Content-Type": "application/json",
            "accept": "application/json",
            'Authorization': `Bearer ${this.user.userToken}`,
            'uuid': uuid
          }
         
        };
        fetch(`https://voicedrive.speakachu.com/voice-memos/${uuid}`, options)
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          this.currentState = data.state;
        });

    },
    loginUser: function() {
      const data = {
        "username": this.userAutentication.userMail,
        "password": this.userAutentication.password
      } 
      const options = {
        method: 'POST',
        headers: {
          "Content-Type": "application/json",
          "accept": "application/json"
        },
        body : JSON.stringify(data)
      };
      fetch('https://voicedrive.speakachu.com/auth', options)
      .then((response) => {
        return response.json();
        
      })
      .then((data) => {
      this.user.userName = `${data.firstName} ${data.lastName}`;
      this.user.userToken = data.token;
      console.log("*************************");
      console.log(typeof this.user.userToken);
      console.log("*************************");
      if(typeof this.user.userToken !== 'undefined') {
        this.loginText = `Welcome ${this.user.userName}`
      } else {
        this.loginText = `Log in!`
      }
      this.retrivingData();
      });

      },
      retrivingData: function(){
        const options = {
          method: 'GET',
          headers: {
            "Content-Type": "application/json",
            "accept": "application/json",
            'Authorization': `Bearer ${this.user.userToken}` 
          }
         
        };
        fetch('https://voicedrive.speakachu.com/voice-memos', options)
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          data.forEach(element => {
            console.log(element);
            this.records.push(
              {
                uuid: element.uuid,
                title: element.title,
                length: element.length,
                date: element.createdAt
              }
            );
          });
          });
        }
     }
  }

</script>

<style lang="scss" scoped>
table {
    background-color: whitesmoke;
    max-width: 90vw;
    margin-top: 5rem;
    margin-bottom: 5rem;
    -webkit-box-shadow: 3px 6px 5px 0px rgba(0,0,0,0.75);
   -moz-box-shadow: 3px 6px 5px 0px rgba(0,0,0,0.75);
    box-shadow: 3px 6px 5px 0px rgba(0,0,0,0.75);
}
</style>



