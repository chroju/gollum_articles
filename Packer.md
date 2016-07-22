* 様々なプラットフォームへ、マシンイメージを作成／管理するツール。
* 対応プラットフォームはAWS（AMI）、DigitalOcean、Docker、VMware vSphereなど。
* イメージ作成にシェルスクリプトの直書きの他、PuppetやAnsibleといったツールも使用できる。

活用記事
----

* [Packer+AnsibleによるAMIの作成 ｜ Developers.IO](http://dev.classmethod.jp/server-side/ansible/build_ami_with_packer_using_ansible/)
  * AMIの管理をAnsibleを使って行う場合の簡単な事例。
* [DockerイメージのビルドにPackerを使うべき理由 | SOTA](http://deeeet.com/writing/2014/03/03/why-building-docker-by-packer/)
  * Dockerfileはロックインになるが、Packerを使うことでプラットフォームに左右されないIaCが実現できるという話。