Linux下如何编译PyQt5-Python2.7

####1. [下载Qt5.4](http://download.qt-project.org/official_releases/qt/5.4/5.4.0/qt-opensource-linux-x86-5.4.0.run)

下载完成后，直接运行安装

####2. [下载最新版的sip](http://pyqt.sourceforge.net/Docs/sip4/)

下载完成后 解压
    
    tar xvf sip-4.16.5.tar.gz
    cd sip-4.16.5
    python  configure.py
    make
    make install

####3. [下载最新版的PyQt5]( http://www.riverbankcomputing.com/software/pyqt/download5)
下载完成后，解压

1.新建cfg文件：

    # The target Python installation.
    py_platform = linux
    py_inc_dir = %(sysroot)/usr/include/python%(py_major).%(py_minor)
    py_pylib_dir = %(sysroot)/usr/lib/python%(py_major).%(py_minor)/config
    py_pylib_lib = python%(py_major).%(py_minor)mu

    # The target PyQt installation.
    pyqt_module_dir = %(sysroot)/usr/lib/python%(py_major)/dist-packages
    pyqt_bin_dir = %(sysroot)/usr/bin
    pyqt_sip_dir = %(sysroot)/usr/share/sip/PyQt5
    pyuic_interpreter = /usr/bin/python%(py_major).%(py_minor)
    pyqt_disabled_features = PyQt_Desktop_OpenGL PyQt_qreal_double

    # Qt configuration common to all versions.
    qt_shared = True

2.编译

    tar xvf PyQt-gpl-5.4.tar.gz
    cd PyQt-gpl-5.4
    python  configure.py --qmake /home/djf/Qt5.4.0/5.4/gcc/bin/qmake --sip-incdir /home/djf/sip-4.16.5/siplib --configuration cfg
    make
    make install

python  configure.py 需要指定--qmake、 --sip-incdir、--configuration

####4. 设置QT_QPA_PLATFORM_PLUGIN_PATH 
在.bashrc或者是.zshrc的尾部添加如下代码
    
    export QT_QPA_PLATFORM_PLUGIN_PATH="/home/djf/Qt5.4.0/5.4/gcc/plugins/"

####5. 运行你的程序
