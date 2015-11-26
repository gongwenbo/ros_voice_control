2015.11.26 wenbo-gong at tarsbot
测试：
(1)安装依赖库： sudo apt-get install gstreamer0.10-pocketsphinx
               sudo apt-get install ros-indigo-audio-common
               sudo apt-get install libasound2
(2)将pocketsphinx包编译
（3）测试：roslaunch pocketsphinx robocup.launch   //如果执行报错 Try apt-get install gstreamer0.10-gconf
          rostopic echo /recognizer/output   //对麦克风说话观察话题数据；

语音库：
  
（1）编译rbx1程序包 
（2）查看语音库：  $roscd pocketsphinx/demo  
                  $more robocup.corpus   
(3)添加语音库： roscd rbx1_speech/config
               more nav_commands.txt
               将nav_commands.txt在http://www.speech.cs.cmu.edu/tools/lmtool-new.html编译生成语音库文件，解压下载的文件，放在rbx1_speech包的config文件夹下
（4）在rbx1_speech/launch文件夹下看看voice_nav_commands.launch这个文件（新的文件名代替nav_commands即可）
     <launch>  
       <node name="recognizer" pkg="pocketsphinx" type="recognizer.py"  
        output="screen">  
       <param name="lm" value="$(find rbx1_speech)/config/nav_commands.lm"/>  
       <param name="dict" value="$(find rbx1_speech)/config/nav_commands.dic"/>  
       </node>  
    </launch> 
