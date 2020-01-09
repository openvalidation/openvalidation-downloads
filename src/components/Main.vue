<template>
  <v-container>
    <v-layout
      wrap
    >

<template>
  <v-card
    :loading="loading"
    class="mx-auto my-12"
    max-width="1024"
    raised
    elevation="24"
  >
    <v-img
      height="250"
      src="/img/openvalidation-banner.png"
    ></v-img>

    <v-card-title>Downloads</v-card-title>
    <v-card-text>
      Just download openVALIDATION CLI and run:
    </v-card-text>

    <v-card-text class="text-left">
      <code flat class="coda flat">curl http://download.openvalidation.io/openvalidation.jar --output openvalidation.jar<br/>
        java -jar openvalidation.jar -r "the name must be Alex" -s "{name:'text'}" -l javascript -e en</code>
    </v-card-text>
    
    <br/>
    
    <v-card-text class="text-center">
        <v-btn rounded outlined class="prim-btns prim" @click="download('openvalidation-cli', '0.0.3')"> <v-icon>mdi-download</v-icon> openvalidation.jar</v-btn>&nbsp;
        <v-btn rounded outlined class="prim-btns" @click="download('openvalidation-openapi', '0.0.3')"> <v-icon>mdi-download</v-icon> openvalidation-openapi.jar</v-btn>
    </v-card-text>

    <br/>

  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left" style="white-space:nowrap">Name</th>
          <th class="text-left">Beschreibung</th>
          <th class="text-left">Version</th>
          <th class="text-left">&nbsp;</th>          
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in maven.artifacts" :key="item.name">
          <td>{{ item.name }}</td>
          <td>
            {{item.description}}
          </td>
          <td>
            <v-combobox
              v-model="selected[item.name]"
              :items="Object.keys(item.versions)"
            ></v-combobox>
          </td>
          <td>
            <v-btn small rounded fab outlined class="dwnld">
              <v-icon>mdi-download</v-icon>
            </v-btn>
          </td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>


    <v-card-actions>

    </v-card-actions>
  </v-card>
</template>


    </v-layout>
  </v-container>
</template>

<script>

import axios from 'axios';

export default {
  name: 'Main',
  methods : {
    download (name, version) {
      var url  =  this.mavenRoot + name + "/" + version + "/" +  name + "-" + version + ".jar";

      window.console.log(url);

      this.downloadWithAxios(url);
    },
    forceFileDownload(response){
      const url = window.URL.createObjectURL(new Blob([response.data]))
      const link = document.createElement('a')
      link.href = url
      link.setAttribute('download', 'file.png') //or any other extension
      document.body.appendChild(link)
      link.click()
    },    

    downloadWithAxios(url){
      axios({
        method: 'get',
        url: url,
        responseType: 'arraybuffer'
      })
      .then(response => {
        
        this.forceFileDownload(response)
        
      })
      .catch(() => window.console.log('error occured'))
    }   
  },
  data: () => ({
    loading:false,
    mavenRoot : "/maven2/io/openvalidation/",
    //mavenRoot : "https://repo1.maven.org/maven2/io/openvalidation/",
    selected : {
        "openvalidation-cli" : "0.0.3",
        "openvalidation-openapi-generator" : "0.0.3",
        "openvalidation-rest" : "0.0.3"
    },
    maven: {
        "name": "openvalidation",
        "artifacts": [
            {
                "name": "openvalidation-cli",
                "description" : "a main cli to run openvalidation as console application.",
                "versions": {
                    "0.0.1": [
                        "openvalidation-cli-0.0.1-javadoc.jar",
                        "openvalidation-cli-0.0.1-javadoc.jar.asc",
                        "openvalidation-cli-0.0.1-javadoc.jar.md5",
                        "openvalidation-cli-0.0.1-javadoc.jar.sha1",
                        "openvalidation-cli-0.0.1-sources.jar",
                        "openvalidation-cli-0.0.1-sources.jar.asc",
                        "openvalidation-cli-0.0.1-sources.jar.md5",
                        "openvalidation-cli-0.0.1-sources.jar.sha1",
                        "openvalidation-cli-0.0.1.jar",
                        "openvalidation-cli-0.0.1.jar.asc",
                        "openvalidation-cli-0.0.1.jar.md5",
                        "openvalidation-cli-0.0.1.jar.sha1",
                        "openvalidation-cli-0.0.1.pom",
                        "openvalidation-cli-0.0.1.pom.asc",
                        "openvalidation-cli-0.0.1.pom.md5",
                        "openvalidation-cli-0.0.1.pom.sha1"
                    ],
                    "0.0.2": [
                        "openvalidation-cli-0.0.2-javadoc.jar",
                        "openvalidation-cli-0.0.2-javadoc.jar.asc",
                        "openvalidation-cli-0.0.2-javadoc.jar.md5",
                        "openvalidation-cli-0.0.2-javadoc.jar.sha1",
                        "openvalidation-cli-0.0.2-sources.jar",
                        "openvalidation-cli-0.0.2-sources.jar.asc",
                        "openvalidation-cli-0.0.2-sources.jar.md5",
                        "openvalidation-cli-0.0.2-sources.jar.sha1",
                        "openvalidation-cli-0.0.2.jar",
                        "openvalidation-cli-0.0.2.jar.asc",
                        "openvalidation-cli-0.0.2.jar.md5",
                        "openvalidation-cli-0.0.2.jar.sha1",
                        "openvalidation-cli-0.0.2.pom",
                        "openvalidation-cli-0.0.2.pom.asc",
                        "openvalidation-cli-0.0.2.pom.md5",
                        "openvalidation-cli-0.0.2.pom.sha1"
                    ],
                    "0.0.3": [
                        "openvalidation-cli-0.0.3-javadoc.jar",
                        "openvalidation-cli-0.0.3-javadoc.jar.asc",
                        "openvalidation-cli-0.0.3-javadoc.jar.md5",
                        "openvalidation-cli-0.0.3-javadoc.jar.sha1",
                        "openvalidation-cli-0.0.3-sources.jar",
                        "openvalidation-cli-0.0.3-sources.jar.asc",
                        "openvalidation-cli-0.0.3-sources.jar.md5",
                        "openvalidation-cli-0.0.3-sources.jar.sha1",
                        "openvalidation-cli-0.0.3.jar",
                        "openvalidation-cli-0.0.3.jar.asc",
                        "openvalidation-cli-0.0.3.jar.md5",
                        "openvalidation-cli-0.0.3.jar.sha1",
                        "openvalidation-cli-0.0.3.pom",
                        "openvalidation-cli-0.0.3.pom.asc",
                        "openvalidation-cli-0.0.3.pom.md5",
                        "openvalidation-cli-0.0.3.pom.sha1"
                    ]
                }
            },
            {
                "name": "openvalidation-openapi-generator",
                "description" : "OpenAPI Generator. Generates validation rules, included within OpenAPI.spec contracts.",
                "versions": {
                    "0.0.1": [
                        "openvalidation-openapi-generator-0.0.1-cli.jar",
                        "openvalidation-openapi-generator-0.0.1-cli.jar.asc",
                        "openvalidation-openapi-generator-0.0.1-cli.jar.md5",
                        "openvalidation-openapi-generator-0.0.1-cli.jar.sha1",
                        "openvalidation-openapi-generator-0.0.1-javadoc.jar",
                        "openvalidation-openapi-generator-0.0.1-javadoc.jar.asc",
                        "openvalidation-openapi-generator-0.0.1-javadoc.jar.md5",
                        "openvalidation-openapi-generator-0.0.1-javadoc.jar.sha1",
                        "openvalidation-openapi-generator-0.0.1-sources.jar",
                        "openvalidation-openapi-generator-0.0.1-sources.jar.asc",
                        "openvalidation-openapi-generator-0.0.1-sources.jar.md5",
                        "openvalidation-openapi-generator-0.0.1-sources.jar.sha1",
                        "openvalidation-openapi-generator-0.0.1-tests.jar",
                        "openvalidation-openapi-generator-0.0.1-tests.jar.asc",
                        "openvalidation-openapi-generator-0.0.1-tests.jar.md5",
                        "openvalidation-openapi-generator-0.0.1-tests.jar.sha1",
                        "openvalidation-openapi-generator-0.0.1.jar",
                        "openvalidation-openapi-generator-0.0.1.jar.asc",
                        "openvalidation-openapi-generator-0.0.1.jar.md5",
                        "openvalidation-openapi-generator-0.0.1.jar.sha1",
                        "openvalidation-openapi-generator-0.0.1.pom",
                        "openvalidation-openapi-generator-0.0.1.pom.asc",
                        "openvalidation-openapi-generator-0.0.1.pom.md5",
                        "openvalidation-openapi-generator-0.0.1.pom.sha1"
                    ]
                }
            },
            {
                "name": "openvalidation-rest",
                "description" : "openVALIDATION as a Service. Run openVALIDATION as REST Service in your own environment.",
                "versions": {
                    "0.0.1": [
                        "openvalidation-rest-0.0.1-javadoc.jar",
                        "openvalidation-rest-0.0.1-javadoc.jar.asc",
                        "openvalidation-rest-0.0.1-javadoc.jar.md5",
                        "openvalidation-rest-0.0.1-javadoc.jar.sha1",
                        "openvalidation-rest-0.0.1-sources.jar",
                        "openvalidation-rest-0.0.1-sources.jar.asc",
                        "openvalidation-rest-0.0.1-sources.jar.md5",
                        "openvalidation-rest-0.0.1-sources.jar.sha1",
                        "openvalidation-rest-0.0.1.jar",
                        "openvalidation-rest-0.0.1.jar.asc",
                        "openvalidation-rest-0.0.1.jar.md5",
                        "openvalidation-rest-0.0.1.jar.sha1",
                        "openvalidation-rest-0.0.1.pom",
                        "openvalidation-rest-0.0.1.pom.asc",
                        "openvalidation-rest-0.0.1.pom.md5",
                        "openvalidation-rest-0.0.1.pom.sha1"
                    ],
                    "0.0.2": [
                        "openvalidation-rest-0.0.2-javadoc.jar",
                        "openvalidation-rest-0.0.2-javadoc.jar.asc",
                        "openvalidation-rest-0.0.2-javadoc.jar.md5",
                        "openvalidation-rest-0.0.2-javadoc.jar.sha1",
                        "openvalidation-rest-0.0.2-sources.jar",
                        "openvalidation-rest-0.0.2-sources.jar.asc",
                        "openvalidation-rest-0.0.2-sources.jar.md5",
                        "openvalidation-rest-0.0.2-sources.jar.sha1",
                        "openvalidation-rest-0.0.2.jar",
                        "openvalidation-rest-0.0.2.jar.asc",
                        "openvalidation-rest-0.0.2.jar.md5",
                        "openvalidation-rest-0.0.2.jar.sha1",
                        "openvalidation-rest-0.0.2.pom",
                        "openvalidation-rest-0.0.2.pom.asc",
                        "openvalidation-rest-0.0.2.pom.md5",
                        "openvalidation-rest-0.0.2.pom.sha1"
                    ],
                    "0.0.3": [
                        "openvalidation-rest-0.0.3-javadoc.jar",
                        "openvalidation-rest-0.0.3-javadoc.jar.asc",
                        "openvalidation-rest-0.0.3-javadoc.jar.md5",
                        "openvalidation-rest-0.0.3-javadoc.jar.sha1",
                        "openvalidation-rest-0.0.3-sources.jar",
                        "openvalidation-rest-0.0.3-sources.jar.asc",
                        "openvalidation-rest-0.0.3-sources.jar.md5",
                        "openvalidation-rest-0.0.3-sources.jar.sha1",
                        "openvalidation-rest-0.0.3.jar",
                        "openvalidation-rest-0.0.3.jar.asc",
                        "openvalidation-rest-0.0.3.jar.md5",
                        "openvalidation-rest-0.0.3.jar.sha1",
                        "openvalidation-rest-0.0.3.pom",
                        "openvalidation-rest-0.0.3.pom.asc",
                        "openvalidation-rest-0.0.3.pom.md5",
                        "openvalidation-rest-0.0.3.pom.sha1"
                    ]
                }
            }
        ]
    }
  }),
};
</script>

<style>
.v-btn {
  text-transform:none !important;
  letter-spacing: normal!important;
  margin:0 10px;
}

.prim-btns, .dwnld {
  color:#05D5FA!important;
}

.prim-btns.prim {
  background-color:#05D5FA!important;
  border-color: transparent;
  color:#fff!important;
}

.coda {
  padding: 25px!important;
  width:100%;
  background-color: #aaa!important;
  color:#fff!important;

  box-shadow: none;
}
</style>
