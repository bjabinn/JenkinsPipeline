pipeline {
  agent any
  parameters {
    choice(choices: 'Maven-3.3.9', description: 'Version of maven to use', name: 'mavenTool')
    choice(choices: "\nfake\nct1\nct2\nct2_loc\ntst_loc\nct2_loc2", description: '', name: 'DATABASE_TARGET')
    booleanParam ( defaultValue: false, description: 'Clean All database', name : 'CLEAN_ALL_DATABASE')
    booleanParam ( defaultValue: false, description: 'Clean CT database', name : 'CLEAN_CT_DATABASE')
    booleanParam ( defaultValue: false, description: 'Clean CT API database', name : 'CLEAN_API_DATABASE')
    booleanParam ( defaultValue: false, description: 'Clean Activiti database', name : 'CLEAN_ACTIVITY_DATABASE')
    booleanParam ( defaultValue: false, description: 'Clean Activiti SRC database', name : 'CLEAN_ACTIVITY_SRC_DATABASE')
    booleanParam ( defaultValue: false, description: 'Clean Product database', name : 'CLEAN_PRODUCT_DATABASE')
    booleanParam ( defaultValue: false, description: 'Clean data warehouse interfaces', name : 'CLEAN_DWH_DATABASE')
    booleanParam ( defaultValue: false, description: 'Run database migration', name : 'RUN_ALL_MIGRATION')
    booleanParam ( defaultValue: false, description: 'Run CT migration', name : 'RUN_CT_MIGRATION')
    booleanParam ( defaultValue: false, description: 'Run CT API migration', name : 'RUN_API_MIGRATION')
    booleanParam ( defaultValue: false, description: 'Run Activiti database migration', name : 'RUN_ACTIVITY_MIGRATION')
    booleanParam ( defaultValue: false, description: 'Run activity SRC database migration', name : 'RUN_ACTIVITY_SRC_MIGRATION')
    booleanParam ( defaultValue: false, description: 'Run Product migration', name : 'RUN_PRODUCT_MIGRATION')
    booleanParam ( defaultValue: false, description: 'Run data warehouse interfaces migration', name : 'RUN_DWH_MIGRATION')
    string(name: 'GIT_REF_DB_MIGRATION', defaultValue: 'develop_everis', description: 'Version of the ema-ct-release to use for DB migrations')
    string(name: 'GIT_REF_EMA_COMMONS', defaultValue: 'develop_everis', description: 'Version of the ema-commons to use for product database')
    string(name: 'GIT_REF_EMA_CT', defaultValue: 'develop_everis', description: 'Version of the ema-ct do you want to use for autority process')
    string(name: 'JENKINS_BUILD_BRANCH', defaultValue: 'master', description: 'Version of this project to use')
  }
  environment {
    CT_DB_URL = 'jdbc:oracle:thin:@192.168.1.11:1522:CTMDEVDB'
    GIT_BASE_URL = 'ssh://git@1.4.1.1:2222/ClinicalTrialRepositories'
    JENKINS_SSH_KEY_NAME = 'jenkins-ssh-key'
    MAVEN_GOAL = 'mvn clean compile -Djava.security.egd=file:/dev/urandom'
    //OFFICE_365_WEBHOOK = 'https://outlook.office.com/webhook/0f9ead0b-b8e0-4a59-a593-2e5db5de76b1@3048dc87-43f0-4100-9acb-ae1971c79395/JenkinsCI/f4e52afeb94d4d7fa27211c964364c89/8c74092d-f563-4787-a644-170f9c6a83cb'
  }
  tools {
    maven "${params.mavenTool}"
  }
  stages{
    stage('Clean the workspace'){
      steps {
        echo 'rm -rf *'
      }
    }
    stage('Variables Setup'){
      steps{
        script {
          if (params.DATABASE_TARGET == "fake")
          {
            CT_DB_USER = 'CT_JENKINS_DB'
            CT_DB_PASSWORD = 'CT_JENKINS_DB'
            CT_API_USER = 'CT_JENKINS_API'
            CT_API_PASSWORD = 'CT_JENKINS_API'
            CT_Activiti_USER = 'CT_JENKINS_Activiti'
            CT_Activiti_PASSWORD = 'CT_JENKINS_Activiti'
            CT_Activiti_SRC_USER = 'CT_JENKINS_SRC_Activiti'
            CT_Activiti_SRC_PASSWORD = 'CT_JENKINS_SRC_Activiti'
            CT_PRODUCT_USER = 'CT_JENKINS_PRODUCT'
            CT_PRODUCT_PASSWORD = 'CT_JENKINS_PRODUCT'
            CT_TABLESPACE = 'CTIS_DATA'
            DWH_USER = 'CT_JENKINS_INTERFACES'
            DWH_PASSWORD = 'CT_JENKINS_INTERFACES'
          } else if(params.DATABASE_TARGET == "ct1")
          {
            CT_DB_USER = 'CT1_DEV_DB'
            CT_DB_PASSWORD = 'CT1_DEV_DB'
            CT_API_USER = 'CT1_DEV_API'
            CT_API_PASSWORD = 'CT1_DEV_API'
            CT_Activiti_USER = 'CT1_DEV_Activiti'
            CT_Activiti_PASSWORD = 'CT1_DEV_Activiti'
            CT_Activiti_SRC_USER = 'CT1_DEV_SRC_Activiti'
            CT_Activiti_SRC_PASSWORD = 'CT1_DEV_SRC_Activiti'
            CT_PRODUCT_USER = 'CTIS_PRODUCT'
            CT_PRODUCT_PASSWORD = 'CTIS_PRODUCT'
            CT_TABLESPACE = 'CTIS_DATA'
            DWH_USER = 'CT1_INTERFACES'
            DWH_PASSWORD = 'CT1_INTERFACES'
          } else if(params.DATABASE_TARGET == "ct2"){
              CT_DB_USER = 'CTIS_DEV_DB'
              CT_DB_PASSWORD = 'CTIS_DEV_DB'
              CT_API_USER = 'CTIS_DEV_API'
              CT_API_PASSWORD = 'CTIS_DEV_API'
              CT_Activiti_USER = 'CTIS_DEV_Activiti'
              CT_Activiti_PASSWORD = 'CTIS_DEV_Activiti'
              CT_Activiti_SRC_USER = 'CTIS_DEV_SRC_Activiti'
              CT_Activiti_SRC_PASSWORD = 'CTIS_DEV_SRC_Activiti'
              CT_PRODUCT_USER = 'CTIS_PRODUCT'
              CT_PRODUCT_PASSWORD = 'CTIS_PRODUCT'
              CT_TABLESPACE = 'CTIS_DATA'
              DWH_USER = 'CTIS_SR_INTERFACES'
              DWH_PASSWORD = 'CTIS_SR_INTERFACES'
          }else if(params.DATABASE_TARGET == "ct2_loc"){
            CT_DB_USER = 'CT2_LOC_DB'
            CT_DB_PASSWORD = 'CT2_LOC_DB'
            CT_API_USER = 'CT2_LOC_API'
            CT_API_PASSWORD = 'CT2_LOC_API'
            CT_Activiti_USER = 'CT2_LOC_Activiti'
            CT_Activiti_PASSWORD = 'CT2_LOC_Activiti'
            CT_Activiti_SRC_USER = 'CT2_LOC_SRC_Activiti'
            CT_Activiti_SRC_PASSWORD = 'CT2_LOC_SRC_Activiti'
            CT_PRODUCT_USER = 'CTIS_PRODUCT'
            CT_PRODUCT_PASSWORD = 'CTIS_PRODUCT'
            CT_TABLESPACE = 'CTIS_DATA'
            DWH_USER = 'CTIS_SR_INTERFACES'
            DWH_PASSWORD = 'CTIS_SR_INTERFACES'
          }else if(params.DATABASE_TARGET == "tst_loc")
          {
            CT_DB_USER = 'CT_TEST_DB'
            CT_DB_PASSWORD = 'CT_TEST_DB'
            CT_API_USER = 'CT_TEST_API'
            CT_API_PASSWORD = 'CT_TEST_API'
            CT_Activiti_USER = 'TST_LOC_ACTIVITI'
            CT_Activiti_PASSWORD = 'TST_LOC_ACTIVITI'
            CT_Activiti_SRC_USER = 'TST_LOC_SRC_ACTIVITI'
            CT_Activiti_SRC_PASSWORD = 'TST_LOC_SRC_ACTIVITI'
            CT_PRODUCT_USER = 'CTIS_PRODUCT'
            CT_PRODUCT_PASSWORD = 'CTIS_PRODUCT'
            CT_TABLESPACE = 'CTIS_DATA'
            DWH_USER = 'CTIS_SR_INTERFACES'
            DWH_PASSWORD = 'CTIS_SR_INTERFACES'
          }else if(params.DATABASE_TARGET == "ct2_loc2")
          {   
            CT_DB_USER = 'CT2_LOC2_DB'
            CT_DB_PASSWORD = 'CT2_LOC2_DB'       
            CT_Activiti_USER = 'CT2_LOC2_ACTIVITY'
            CT_Activiti_PASSWORD = 'CT2_LOC2_ACTIVITY'  
            CT_Activiti_SRC_USER = 'CT2_LOC2_SRC_Activiti'
            CT_Activiti_SRC_PASSWORD = 'CT2_LOC2_SRC_Activiti'          
            CT_TABLESPACE = 'CTIS_DATA'
            DWH_USER = 'CTIS_SR_INTERFACES'
            DWH_PASSWORD = 'CTIS_SR_INTERFACES'
          }          
        }
      //office365ConnectorSend message: "DB migraitons started for ${env.BRANCH_NAME}", status:"Started", webhookUrl:"${OFFICE_365_WEBHOOK}"
      }
    }
      // stage('Code Checkout'){
      //   failFast true
      //   parallel {
      //     stage('CO-ema-commons'){
      //       steps{
      //         gitCheckout("ema-commons","ema-commons","$GIT_REF_EMA_COMMONS")
      //       }
      //     }
      //     stage('CO-ema-ct-migration'){
      //       steps{
      //         gitCheckout("ema-ct-migration","ema-ct-migration","$GIT_REF_DB_MIGRATION")
      //       }
      //     }
      //     stage('CO-ema-ct'){
      //       steps{
      //         gitCheckout("ema-ct","ema-ct","$GIT_REF_EMA_CT")
      //       }
      //     }
      //   }
      // }
      stage ('Product DB Clean'){
        when { expression { return params.CLEAN_PRODUCT_DATABASE || params.CLEAN_ALL_DATABASE } }
        steps{
          dir('ema-commons'){
            echo """
            $MAVEN_GOAL -f ema-commons-pd/ema-commons-pd-db-migration  \
            -Pproducts-clean -Dproducts.database.username=${CT_PRODUCT_USER} \
            -Dproducts.database.password=${CT_PRODUCT_PASSWORD}-Dproducts.database.url=${CT_DB_URL}
            """
          }
        }
      }
      stage ('Product DB Migration'){
        when { expression { return params.RUN_PRODUCT_MIGRATION || params.RUN_ALL_MIGRATION } }
        steps{
          dir('ema-commons'){
            echo """
            $MAVEN_GOAL -f ema-commons-pd/ema-commons-pd-db-migration  \
            -Pproducts-migrate -Dproducts.database.username=${CT_PRODUCT_USER} \
            -Dproducts.database.password=${CT_PRODUCT_PASSWORD} -Dproducts.database.url=${CT_DB_URL}
            """
          }
        }
      }
      stage ('CT DB Clean'){
        when { expression { return params.CLEAN_CT_DATABASE || params.CLEAN_ALL_DATABASE } }
        steps{
          runDatabaseMigration("$CT_DB_USER","$CT_DB_PASSWORD",'application-clean','ct.app','ema-ct-application-migration/pom.xml','')
        }
      }
      stage ('CT API Clean'){
        when { expression { return params.CLEAN_API_DATABASE || params.CLEAN_ALL_DATABASE } }
        steps{
          runDatabaseMigration("$CT_API_USER","$CT_API_PASSWORD",'application-clean','ct.app','ema-ct-application-migration/pom.xml','')
        }
      }
      stage ('Activiti DB Clean'){
        when { expression { return params.CLEAN_ACTIVITY_DATABASE || params.CLEAN_ALL_DATABASE } }
        steps{
          runDatabaseMigration("$CT_Activiti_USER","$CT_Activiti_PASSWORD",'activiti-clean','ct.act','ema-ct-activiti-migration/pom.xml','')
        }
      }
      stage ('Activiti SRC DB Clean'){
        when { expression { return params.CLEAN_ACTIVITY_SRC_DATABASE || params.CLEAN_ALL_DATABASE } }
        steps{
          runDatabaseMigration("$CT_Activiti_SRC_USER","$CT_Activiti_SRC_PASSWORD",'activiti-clean','ct.act','ema-ct-activiti-migration/pom.xml','')
        }
      }
      stage('Data Warehouse DB Clean') {
        when { expression { return params.CLEAN_DWH_DATABASE || params.CLEAN_ALL_DATABASE } }
        steps {
          runDatabaseMigration("$DWH_USER","$DWH_PASSWORD",'application-clean','ct.dwh','ema-ct-dwh-migration/pom.xml','')
        }
      }
      stage ('CT DB Migration'){
        when { expression { return params.RUN_ALL_MIGRATION || params.RUN_CT_MIGRATION } }
        steps {
          runDatabaseMigration("$CT_DB_USER","$CT_DB_PASSWORD",'application-migrate','ct.app','ema-ct-application-migration/pom.xml',"$CT_DB_USER")
        }
      }
      stage ('CT Api Migration'){
        when { expression { return params.RUN_ALL_MIGRATION || params.RUN_API_MIGRATION } }
        steps {
          runDatabaseMigration("$CT_API_USER","$CT_API_PASSWORD",'application-migrate','ct.app','ema-ct-application-migration/pom.xml',"$CT_API_USER")
          runDatabaseMigration("$CT_API_USER","$CT_API_PASSWORD",'public-migrate','ct.pub','ema-ct-public-migration/pom.xml',"$CT_API_USER")
        }
      }
      stage ('Activiti DB Migration'){
        when { expression { return params.RUN_ALL_MIGRATION || params.RUN_ACTIVITY_MIGRATION } }
        steps {
          runDatabaseMigration("$CT_Activiti_USER","$CT_Activiti_PASSWORD",'activiti-migrate','ct.act','ema-ct-activiti-migration/pom.xml',"$CT_DB_USER")
          runActivitiProcessMigration("$CT_Activiti_USER","$CT_Activiti_PASSWORD",'process-deploy-ct')
        }
      }
      stage ('Activiti SRC DB Migration'){
        when { expression { return params.RUN_ALL_MIGRATION || params.RUN_ACTIVITY_SRC_MIGRATION } }
        steps {
          runDatabaseMigration("$CT_Activiti_SRC_USER","$CT_Activiti_SRC_PASSWORD",'activiti-migrate','ct.act','ema-ct-activiti-migration/pom.xml',"$CT_DB_USER")
          runActivitiProcessMigration("$CT_Activiti_SRC_USER","$CT_Activiti_SRC_PASSWORD",'process-deploy-src')
        }
      }
      stage('Data Warehouse DB migration') {
        when { expression { return params.RUN_ALL_MIGRATION || params.RUN_DWH_MIGRATION } }
        steps {
          runDatabaseMigration("$DWH_USER","$DWH_PASSWORD",'application-migrate','ct.dwh','ema-ct-dwh-migration/pom.xml',"$CT_DB_USER")
        }
      }
    }
  }
  void runDatabaseMigration(db_user,db_password,profile_name,db_var_prefix,pom_file,ctcs_placeholder){
    dir('ema-ct-migration'){
      echo """
      ${MAVEN_GOAL} -f ${pom_file} -P${profile_name} \
      -D${db_var_prefix}.database.url=${CT_DB_URL} \
      -D${db_var_prefix}.database.username=${db_user} \
      -D${db_var_prefix}.database.password=${db_password}  \
      -Dflyway.placeholders.CTCS=${ctcs_placeholder} \
      -Dflyway.placeholders.CTCS_INTERFACES=${DWH_USER} \
      -Dflyway.placeholders.TABLESPACE=${CT_TABLESPACE}
      """
    }
  }

  void runActivitiProcessMigration(db_user,db_password,profile_name){
    dir('ema-ct'){
      echo """
      mvn -f 'ct-authority/ct-authority-activiti/pom.xml' package -P${profile_name} \
      -DskipTests -Dct-activiti.db.url=${CT_DB_URL} -Dactiviti.db.user=${db_user} \
      -Dactiviti.db.password=${db_password}
      """
    }
  }

  // void gitCheckout(dir_name,project_name,git_release){
  //   dir("${dir_name}"){
  //     checkout([$class: 'GitSCM',
  //     branches: [[name: "${git_release}"]],
  //     userRemoteConfigs:
  //     [[
  //     url: "${GIT_BASE_URL}/${project_name}.git",
  //     credentialsId: "${JENKINS_SSH_KEY_NAME}"
  //     ]]
  //     ])
  //   }
  // }
