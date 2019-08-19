pipeline {
    agent any
    parameters {
    string(name: 'node_linux', defaultValue: 'linux01', description: '')
    string(name: 'input_file_linux', defaultValue: 'test_input01.txt', description: '')
    string(name: 'path_input_linux', defaultValue: '/home/birdmodify/testing/input/', description: '')
    string(name: 'input_file_window', defaultValue: 'pipeline_palm.txt', description: '')
    string(name: 'path_input_windows', defaultValue: "C:\\Users\\Admin\\Documents\\output", description: '')
    string(name: 'ERROR', defaultValue: 'ERROR1', description: '')
    string(name: 'gen_filename', defaultValue: 'test_wrap.txt', description: '')
    string(name: 'time_dalay', defaultValue: '3', description: '')
    string(name: 'status', defaultValue: 'success', description: '')
    string(name: 'is_gen_file', defaultValue: 'yes', description: '')
    choice(name: 'choice_run', choices: ['run_all', 'run_stage1', 'run_stage2', 'run_stage3', 'run_stage4', 'run_stage5', 'run_stage6', 'run_stage7', 'run_stage8', 'run_stage9', 'run_stage10', 'run_stage11', 'run_stage12', 'run_stage13', 'run_stage14', 'run_stage15', 'run_stage16'], description: '')
  }
    stages{
        stage('Step1'){
            steps {
                node('master'){
                    script {
                        if("$choice_run" == "run_all" || "$choice_run" == "run_stage1"){
                            echo "step1 path window"
                            build 'Clear_path_by_compress_job1'
                            build job: 'Check_input_files_windows', parameters: [string(name: 'Path_folder', value: "$path_input_windows"), string(name: 'file_input', value: "$input_file_window")]
                            build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                            ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                            if (ch_log_win == "SUCCESS") {
                                error 'Failed, exiting now...'
                            }
                        }else {
                            not "bypass"
                        }
                    }
                }
                node("$node_linux") {
                    script {
                        if ("$choice_run" == "run_all" || "$choice_run" == "run_stage1") {
                            echo "Stap1 path linux"
                            build job: 'Check_input_files_linux', parameters: [string(name: 'input_file_linux', value: "$input_file_linux"), string(name: 'Path_input', value: "$path_input_linux")]
                            def check = fileExists("$path_input_linux$input_file_linux")
                            if (check) {
                                  fileOperations([folderCopyOperation(destinationFolderPath: '/home/birdmodify/testing/back_up/', sourceFolderPath: '/home/birdmodify/testing/output/')])
                            }else {
                                echo "false"
                            }
                        } else {
                            echo "bypass"
                        }
                    }
                }
            }
        }
        stage('Step2'){
            steps {
                node('master'){
                    script {
                        if ("$choice_run" == "run_all" || "$choice_run" == "run_stage2") {
                            echo "step2 path window"
                            build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                            ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                            if (ch_log_win == "SUCCESS") {
                                error 'Failed, exiting now...'
                            }
                            def checkfile = fileExists('C:\\Users\\Admin\\Documents\\output\\test_wrap.txt')
                            TimeZone.getTimeZone('UTC')
                            Date date= new Date()
                            String newdate=date.format("YYYY-MM-DD_HH-mm-ss-Ms")
                            String textdate = newdate+".zip"
                            if (checkfile){
                                build job: 'zipfile_win', parameters: [string(name: 'path_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'name_file_output', value: "$textdate")]
                            }else{
                                error 'Failed, exiting now...'
                            }
                        } else {
                            not "bypass"
                        }
                    }
                }
            }
        }
        stage('Step3'){
            steps {
                node('master'){
                    script {
                        if ("$choice_run" == "run_all" || "$choice_run" == "run_stage3") {
                            echo "step3 path window"
                            build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                            ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                            if (ch_log_win == "SUCCESS") {
                                error 'Failed, exiting now...'
                            }
                        } else {
                            echo "bypass"
                        }
                    }
                }
                node("$node_linux") {
                    script {
                        echo "Stap3 path linux"
                        def check_input = fileExists("/home/birdmodify/testing/input/${input_file_linux}")
                            if (check_input) {
                                echo "folder is not Empty"
                            } else {
                                echo "folder is empty"
                                sh '''cd /home/birdmodify/testing/input/
                                touch $test_input01
                                touch $test_input02
                                touch $test_input03
                                '''
                            }
                        def check = fileExists("/home/birdmodify/testing/output/test_output01.txt") 
                        if (check) {
                            echo "Succress"
                        } else {
                            error 'Failed, exiting now...'
                        }
                    }
                }
            }
        }
        stage('Step4'){
            steps {
                node('master'){
                    script {
                        echo "step4 path window"
                        build job: 'Check_input_files_windows', parameters: [string(name: 'Path_folder', value: "$path_input_windows"), string(name: 'file_input', value: "$input_file_window")]
                        build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                        ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                        if (ch_log_win == "SUCCESS") {
                            error 'Failed, exiting now...'
                        }
                    }
                }
                node("$node_linux") {
                    script {
                        echo "Stap4 path linux"
                        def check = fileExists("/home/birdmodify/testing/output/test_output01.txt") 
                        if (check) {
                            echo "Succress"
                        } else {
                            error 'Failed, exiting now...'
                        }
                    }
                }
            }
        }
        stage('Step5'){
            steps {
                node('master'){
                    script {
                        echo "step5 path window"
                        build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                        ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                        if (ch_log_win == "SUCCESS") {
                            error 'Failed, exiting now...'
                        }
                    }
                }
                node("$node_linux") {
                    script {
                        echo "Stap5 path linux"
                        def check_input = fileExists("/home/birdmodify/testing/input/${input_file_linux}")
                            if (check_input) {
                                echo "folder is not Empty"
                            } else {
                                echo "folder is empty"
                                sh '''cd /home/birdmodify/testing/input/
                                touch $test_input01
                                touch $test_input02
                                touch $test_input03
                                '''
                            }
                        def check = fileExists("/home/birdmodify/testing/output/test_output01.txt") 
                        if (check) {
                            echo "Succress"
                        } else {
                            error 'Failed, exiting now...'
                        }
                    }
                }
            }
        }
        stage('Step6'){
            steps {
                node('master') {
                    script {
                        echo "Stap6 path window"
                       build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                        ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                        if (ch_log_win == "SUCCESS") {
                            error 'Failed, exiting now...'
                        }
                    }
                }
                node("$node_linux") {
                    script {
                        echo "Stap6 path linux"
                        def check_input = fileExists("/home/birdmodify/testing/input/${input_file_linux}")
                            if (check_input) {
                                echo "folder is not Empty"
                            } else {
                                echo "folder is empty"
                                sh '''cd /home/birdmodify/testing/input/
                                touch $test_input01
                                touch $test_input02
                                touch $test_input03
                                '''
                            }
                        def check = fileExists("/home/birdmodify/testing/output/test_output01.txt") 
                        if (check) {
                            echo "Succress"
                        } else {
                            error 'Failed, exiting now...'
                        }
                        fileOperations([folderCopyOperation(destinationFolderPath: '/home/birdmodify/testing/back_up/', sourceFolderPath: '/home/birdmodify/testing/output/')])
                    }
                }
            }
        }
        stage('Step7'){
            steps {
                node('master') {
                    script {
                        echo "Stap7 path window"
                        build job: 'Check_input_files_windows', parameters: [string(name: 'Path_folder', value: "$path_input_windows"), string(name: 'file_input', value: "$input_file_window")]
                        build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                        ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                        if (ch_log_win == "SUCCESS") {
                            error 'Failed, exiting now...'
                        }
                    }
                }
                node("$node_linux") {
                    script {
                        echo "Stap7 path linux"
                        def check = fileExists("/home/birdmodify/testing/output/test_output01.txt") 
                        if (check) {
                            echo "Succress"
                        } else {
                            error 'Failed, exiting now...'
                        }
                        fileOperations([folderCopyOperation(destinationFolderPath: '/home/birdmodify/testing/back_up/', sourceFolderPath: '/home/birdmodify/testing/output/')])
                        sh label: '', script: '''cd /home/birdmodify/testing
                        zip -r output.zip output
                        '''
                    }
                }
            }
        }
        stage('Step8'){
            steps {
                node('master'){
                    script {
                        echo "Stap8 path window"
                        build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                        ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                        if (ch_log_win == "SUCCESS") {
                            error 'Failed, exiting now...'
                        }
                    }
                }
                node("$node_linux") {
                    script {
                        echo "Stap8 path linux"
                        def check = fileExists("/home/birdmodify/testing/output/test_output01.txt") 
                        if (check) {
                            echo "Succress"
                        } else {
                            error 'Failed, exiting now...'
                        }
                        fileOperations([folderCopyOperation(destinationFolderPath: '/home/birdmodify/testing/back_up/', sourceFolderPath: '/home/birdmodify/testing/output/')])
                    }
                }
            }
        }
        stage('Step9'){
            steps {
                node('master') {
                    script {
                        echo "Step9 path window"
                        build job: 'Check_input_files_windows', parameters: [string(name: 'Path_folder', value: "$path_input_windows"), string(name: 'file_input', value: "$input_file_window")]
                        build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                        ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                        if (ch_log_win == "SUCCESS") {
                            error 'Failed, exiting now...'
                        }
                    }
                }
                node("$node_linux") {
                    script {
                        echo "Stap9 path linux"
                        def check_input = fileExists("/home/birdmodify/testing/input/${input_file_linux}")
                            if (check_input) {
                                echo "folder is not Empty"
                            } else {
                                echo "folder is empty"
                                sh '''cd /home/birdmodify/testing/input/
                                touch $test_input01
                                touch $test_input02
                                touch $test_input03
                                '''
                            }
                        def check = fileExists("/home/birdmodify/testing/output/test_output01.txt") 
                        if (check) {
                            echo "Succress"
                        } else {
                            error 'Failed, exiting now...'
                        }
                    }
                }
            }
        }
        stage('Step10'){
            steps {
                node('master') {
                    script {
                        echo "Step10 path window"
                        build job: 'Check_input_files_windows', parameters: [string(name: 'Path_folder', value: "$path_input_windows"), string(name: 'file_input', value: "$input_file_window")]
                        build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                        ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                        if (ch_log_win == "SUCCESS") {
                            error 'Failed, exiting now...'
                        }
                        build job: 'Check_output_files_windows', parameters: [string(name: 'file_name', value: "$gen_filename"), string(name: 'path_output_window', value: 'C:\\Users\\Admin\\Documents\\output')]
                        fileOperations([folderCopyOperation(destinationFolderPath: 'C:\\Users\\Admin\\Documents\\backup', sourceFolderPath: 'C:\\Users\\Admin\\Documents\\output')])
                    }
                }
                node("$node_linux") {
                    script {
                        echo "Stap10 path linux"
                        def check_input = fileExists("/home/birdmodify/testing/input/${input_file_linux}")
                            if (check_input) {
                                echo "folder is not Empty"
                            } else {
                                echo "folder is empty"
                                sh '''cd /home/birdmodify/testing/input/
                                touch $test_input01
                                touch $test_input02
                                touch $test_input03
                                '''
                            }
                        def check = fileExists("/home/birdmodify/testing/output/test_output01.txt") 
                        if (check) {
                            echo "Succress"
                        } else {
                            error 'Failed, exiting now...'
                        }
                    }
                }
            }
        }
        stage('Step11'){
            steps {
                node('master') {
                    script {
                        echo "Stap11 path window"
                        build job: 'Check_input_files_windows', parameters: [string(name: 'Path_folder', value: "$path_input_windows"), string(name: 'file_input', value: "$input_file_window")]
                        build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                        ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                        if (ch_log_win == "SUCCESS") {
                            error 'Failed, exiting now...'
                        }
                    }
                }
                node("$node_linux") {
                    script {
                        echo "Stap11 path linux"
                        def check = fileExists("/home/birdmodify/testing/output/test_output01.txt") 
                        if (check) {
                            echo "Succress"
                        } else {
                            error 'Failed, exiting now...'
                        }
                    }
                }
            }
        }
        stage('Step12'){
            steps {
                node('master'){
                    script {
                        echo "Step12 path window"
                        build job: 'Check_input_files_windows', parameters: [string(name: 'Path_folder', value: "$path_input_windows"), string(name: 'file_input', value: "$input_file_window")]
                        build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                        ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                        if (ch_log_win == "SUCCESS") {
                            error 'Failed, exiting now...'
                        }
                        build job: 'Check_output_files_windows', parameters: [string(name: 'file_name', value: "$gen_filename"), string(name: 'path_output_window', value: 'C:\\Users\\Admin\\Documents\\output')]
                    }
                }
                node("$node_linux") {
                    script {
                        echo "Stap12 path linux"
                        def check_input = fileExists("/home/birdmodify/testing/input/${input_file_linux}")
                            if (check_input) {
                                echo "folder is not Empty"
                            } else {
                                echo "folder is empty"
                                sh '''cd /home/birdmodify/testing/input/
                                touch $test_input01
                                touch $test_input02
                                touch $test_input03
                                '''
                            }
                        def check = fileExists("/home/birdmodify/testing/output/test_output01.txt") 
                        if (check) {
                            echo "Succress"
                            fileOperations([folderCopyOperation(destinationFolderPath: '/home/birdmodify/testing/back_up/', sourceFolderPath: '/home/birdmodify/testing/output/')])
                        } else {
                            error 'Failed, exiting now...'
                        }
                        sh label: '', script: '''cd /home/birdmodify/testing
                        zip -r output.zip output
                        '''
                    }
                }
            }
        }
        stage('Step13'){
            steps {
                node('master') {
                    script {
                        echo "Stap13 path window"
                        build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                        ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                        if (ch_log_win == "SUCCESS") {
                            error 'Failed, exiting now...'
                        }
                    }
                }
                node("$node_linux") {
                    script {
                        echo "Stap13 path linux"
                        def check = fileExists("/home/birdmodify/testing/output/test_output01.txt") 
                        if (check) {
                            echo "Succress"
                        } else {
                            error 'Failed, exiting now...'
                        }
                    }
                }
            }
        }
        stage('Step14'){
            steps {
                node('master') {
                    script {
                        echo "Stap14 path window"
                        build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                        ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                        if (ch_log_win == "SUCCESS") {
                            error 'Failed, exiting now...'
                        }
                        build job: 'Check_output_files_windows', parameters: [string(name: 'file_name', value: "$gen_filename"), string(name: 'path_output_window', value: 'C:\\Users\\Admin\\Documents\\output')]
                    }
                }
                node("$node_linux") {
                    script {
                        echo "Stap14 path linux"
                        def check_input = fileExists("/home/birdmodify/testing/input/${input_file_linux}")
                            if (check_input) {
                                echo "folder is not Empty"
                            } else {
                                echo "folder is empty"
                                sh '''cd /home/birdmodify/testing/input/
                                touch $test_input01
                                touch $test_input02
                                touch $test_input03
                                '''
                            }
                        def check = fileExists("/home/birdmodify/testing/output/test_output01.txt") 
                        if (check) {
                            echo "Succress"
                        } else {
                            error 'Failed, exiting now...'
                        }
                    }
                }
            }
        }
        stage('Step15'){
            steps {
                node('master') {
                    script {
                        echo "Stap15 path window"
                        build job: 'Execute_sas_windows', parameters: [string(name: 'folder_sas', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\script'), string(name: 'path_output_folder', value: 'C:\\Users\\Admin\\Documents\\output'), string(name: 'Filename', value: "$gen_filename"), string(name: 'time', value: "$time_dalay"), string(name: 'status', value: "$status"), string(name: 'is_generate_file', value: "$is_gen_file")]
                        ch_log_win = build(job: 'Analyze log files at windows', parameters: [string(name: 'Path_folder', value: 'C:\\Users\\Admin\\Documents\\scb\\Linux\\Logs'), string(name: 'Check_File', value: 'EDC_Merchant.log'), string(name: 'ERROE_STR', value: "$ERROR")], propagate: false, quietPeriod: 3, wait: true).result
                        if (ch_log_win == "SUCCESS") {
                            error 'Failed, exiting now...'
                        }
                    }
                }
                node("$node_linux") {
                    script {
                        echo "Stap15 path linux"
                        def check_input = fileExists("/home/birdmodify/testing/input/${input_file_linux}")
                            if (check_input) {
                                echo "folder is not Empty"
                            } else {
                                echo "folder is empty"
                                sh '''cd /home/birdmodify/testing/input/
                                touch $test_input01
                                touch $test_input02
                                touch $test_input03
                                '''
                            }
                        def check = fileExists("/home/birdmodify/testing/output/test_output01.txt") 
                        if (check) {
                            echo "Succress"
                        } else {
                            error 'Failed, exiting now...'
                        }
                    }
                }
            }
        }
    }
}
