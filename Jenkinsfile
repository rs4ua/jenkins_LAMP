pipeline {
    agent { label 'local-agent' }
    environment {
        ANSIBLE_USER = 'user'
        ANSIBLE_SUDO_PASS = 'roMashka'
        ANSIBLE_SSH_PRIVATE_KEY = '''
        -----BEGIN OPENSSH PRIVATE KEY-----
        b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn
        NhAAAAAwEAAQAAAYEA3X4vCrlyqtTioHLpxHrb43JelQIPAQ+VBlb4uIaZSUJRcHR2O9il
        YA34rFSpUklMnCTIk/61HU1GUc83CXGSxgzTg+mLNAVqf1QfGZOhr2+lNuV/FujcrSb2PD
        DSGWs+LUyZfzRgUre6I3oFgVSDfAejQBP4hWVRy61iu5J5aAwESTPJrzqmzsq1Q1GU+0P9
        3nVhcB0elgLcEU44av3MSo6yy71Py4EZIeACCbWAkmV+KnMhhn5yReBU5cEyhCX9wgAN6p
        FIe0ACAghY19Dt3RX30QZX3jhwncDQrUd/Y+R9Ssg+ahaV5mmfZBcXg1LRVj5SkrQOdZ3L
        GasD0ZpsmRzJiFrfqioGW2Oh4XeSWBEStymLBVgyd4LxjAvM9+2fMFdYCJbajuPU9NXUx/
        LttqOVy78EkZRtIU3c9mmje3M1hA0RJbb6XEJnHsgqzZON0nqWKO5tw+j9pJ6940ybvzki
        Sue5fzRkQSIy+amRvBsNrG76LzSaH7XkMChatHpFAAAFgNKS+9/SkvvfAAAAB3NzaC1yc2
        EAAAGBAN1+Lwq5cqrU4qBy6cR62+NyXpUCDwEPlQZW+LiGmUlCUXB0djvYpWAN+KxUqVJJ
        TJwkyJP+tR1NRlHPNwlxksYM04PpizQFan9UHxmToa9vpTblfxbo3K0m9jww0hlrPi1MmX
        80YFK3uiN6BYFUg3wHo0AT+IVlUcutYruSeWgMBEkzya86ps7KtUNRlPtD/d51YXAdHpYC
        3BFOOGr9zEqOssu9T8uBGSHgAgm1gJJlfipzIYZ+ckXgVOXBMoQl/cIADeqRSHtAAgIIWN
        fQ7d0V99EGV944cJ3A0K1Hf2PkfUrIPmoWleZpn2QXF4NS0VY+UpK0DnWdyxmrA9GabJkc
        yYha36oqBltjoeF3klgRErcpiwVYMneC8YwLzPftnzBXWAiW2o7j1PTV1Mfy7bajlcu/BJ
        GUbSFN3PZpo3tzNYQNESW2+lxCZx7IKs2TjdJ6lijubcPo/aSeveNMm785IkrnuX80ZEEi
        MvmpkbwbDaxu+i80mh+15DAoWrR6RQAAAAMBAAEAAAGAHYPzZlk0kdW5FnsBskxR8YL73h
        zuXWyTZgsgbUyIcDX9bsAiQlLaJMzv0p0cjCnW4ubW8LvMLEmwIXY8xg4jqi8q34T3ZxkC
        qlGOLGUbMmrtB/34m9evkoZi4T37PWZoXHZ87PHQlS1FCXW49pVJyTUmWMNghnwsNHlYMx
        kvgwE47/1N9sMY1+00zvH36azTj3myYJOM0B4077xt8bn854GRC2vgjoSXUgeNFfihF8Ed
        GTCK6uZ+OVgN0CkY33nFUcOuzsbGmUhI7jP2T/XpGJ6DxaErS+oHthHl34R51lQRuHB6ag
        q+uBt6RlJYAARO7lTcJZBgORbcyZ1W1RQbN4CDL9eILJADlnKqYczMplSvNIWsYstQMV/b
        B8FxlYANJDqvW+s3XoJxz5zGpcOfikAUVKIYl9MK5ex1TdEO0Zb/QFakOhCet5sxolpAFj
        94VueG28ZoTkx6tEFbhK94KqlfT9E1MACQWFg/vaIyhB3/iggfWjCchDMrOpTLF8M5AAAA
        wD+HhoJRPwVeGg1+9f1Lc+/jmHXinjbQ2b6KWnGm9MxPcpetCqwbX/YR2oboz4b1C3n9hG
        syAIDJTcyPe5iHMp31L+9CBkrsqDtDoVAUvcZY+lkWdM3Noe+nIfSkPDS7EHYCErOjxSn9
        IizGoNnBOAt5Iaqha76tv0hAQ0iSkQYdiEg0wmE8kca74cHxiz8PJdd3VRQCJI40A4ADeV
        Tl8eZsuTsfME87oKehZEMf3ZEGqfvCxnnsHNp0b9zy2yHqugAAAMEA8oAYT7RuVleS6igH
        zTa6dCNasXm04oP4F9kRzpq0OmQDawn7iMRnhgIKA7ilK5C3vUsrLDoE0NH1d1wbCbvHvm
        gEK7T3IeFrKU0dwI7N5iSzfiYJOCHDh8ojG2vonNVVP3UOMQzzx/20La3zqRfJrmPLfuzR
        9Z5OMyADhySWfERvZ3zJIf/HJBO8Kr2heSLSaTxJcOa92H+kEF1KGuqiF3eckCoAwlWAky
        8Kr3F+6Fg7T+YY/dgxJS2yKffV6vApAAAAwQDp0rVnG5JNkZ+zy+3CelXs6alomYeBxjOe
        jBPOtgRSRaK25Y15d4EB9Xhve9iCy7G8itBi2TlcAke4zW1HcVsA9AX+nLBX6UZuHxShFz
        64sL2L9Yjd93YmOJ1wh7LY7sbwaaWrhcoHV56cWxqf6DK+bXU6DjAes67hpuJrHl4ykSG/
        6FQ/KtrGVQvkD73HVP3pcuUFjkixuNUtzdUwfxZuA9gq3R2xnUTPyCq/k5PrvwVlHITvUb
        vnb7Lt4X/tTL0AAAALdXNlckBnaXRzcnY=
        -----END OPENSSH PRIVATE KEY-----
        '''
        ANSIBLE_HOST_KEY_CHECKING = 'false'
    }
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Prepare SSH Key') {
            steps {
                script {
                    // Write the private key to a file
                    writeFile file: 'ansible_/private_key.pem', text: "${ANSIBLE_SSH_PRIVATE_KEY}"
                    // Set proper permissions for the private key file
                    sh 'chmod 600 ansible_/private_key.pem'
                }
            }
        }
        stage('Run Ansible Playbook') {
            steps {
                script {
                    // Running ansible-playbook with the specified private key
                    sh 'ansible-playbook -i ansible_/hosts.txt --private-key ansible_/private_key.pem ansible_/ansible-playbook.yml'
                }
            }
        }
    }
    post {
        failure {
            echo 'Ansible playbook execution failed!'
        }
    }
}
