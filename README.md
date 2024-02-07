# practice_jenkins_build
practice trigger project build on jenkins with github

# Practice Steps
- github → jenkins
    - Flow : commit code to github → jenkins build → return build result to github
    - Git project : [https://github.com/alexho0205/practice_jenkins_build](https://github.com/alexho0205/practice_jenkins_build)
    - Steps
        1. create personal token on github ( settings → developer settings )
        2. add github server on  jenkins ( system → github servers )
            1. put personal token to credential ( credential type = secret text )
        3. create ssh-key pair
        4. put public key on github ( profile → settings → ssh and GPG keys → add ssh keys )
        5. put private key on jenkins ( credentials → add credentials → ssh with private key )
        6. add webhook on github ( 
            1. url → ```${jenkins_url}```/github-webhoook/
            2. content type → json
        7. create free-style job (jenkins)
        8. trigger jenkins to build project : commit code directly (github)
        9. check build result on github : repo -> commits -> green check (綠色小勾勾）
    - Bug Fix
        - 如果 jenkins  是全新的，第一次連線 [github.com](http://github.com) 前，需要加入 host key
            - ( linux )ssh 登入到 jenkins ，切換身份到 jenkins
                
                ```bash
                # 切換身份
                $ sudo su jenkins
                # 連線github.com，請自行變更 repo 位置
                # 連線後，linux 發現沒有 github.com 的 host key
                # 尋問是否加入 -> YES
                $ git ls-remote -h -- git@github.com:alexho0205/practice_jenkins_build.git HEAD
                ```
        - jenkins 需要外部IP，可使用ngrok
