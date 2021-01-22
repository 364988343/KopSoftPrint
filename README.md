## 项目介绍
****
* KopSoft标签(条码)打印软件 http://print.kopsoft.cn/
* Gitee https://gitee.com/williamyang3/KopSoftPrint
* GitHub https://github.com/williamyang3/KopSoftPrint
*
* KopSoft仓库管理系统 http://wms.kopsoft.cn/
* Gitee https://gitee.com/yulou/KopSoftWms
* GitHub https://github.com/lysilver/KopSoftWms
*
* KopSoft制造执行系统 http://mes.kopsoft.cn/
* Gitee https://gitee.com/yulou/KopSoftMES
* GitHub https://github.com/lysilver/KopSoftMES
*
* KopSoft数据采集与监控,电子看板,Andon安灯系统 http://kanban.kopsoft.cn/
* Gitee https://gitee.com/williamyang3/KopSoftSCADA
* GitHub https://github.com/williamyang3/KopSoftSCADA
*
* 技术QQ群:421635 商务合作:13921987606
****

## 技术
Microsoft .NET Framework 4.5
ZXing.Net
C#打印
1.建立PrintDocument对象
2.设置PrintPage打印事件
3.调用Print方法进行打印

BarcodeWriter用于生成图片格式的条码类，通过Write函数进行输出
BarcodeFormat枚举类型，条形码/二维码
QrCodeEncodingOptions二维码设置选项，继承于EncodingOptions，主要设置宽，高，编码方式等
MultiFormatWriter复合格式条码写码器，通过encode方法得到BitMatrix
BitMatrix表示按位表示的二维矩阵数组，元素的值用true和false表示二进制中的1和0

支持文本、图片、条形码、二维码、直线等对象自由拖拽、删除，纸张尺寸边距设计等，
并可保存为XML模板，可直接打印到打印机，数据源支持XML、EXCEL、数据库等

## 操作步骤
* 1.纸张设置：选择纸张尺寸或自定义纸张尺寸
* 2.条形码；二维码；图片；文本；直线；设置好属性后 插入到编辑界面
* 3.各对象支持拖拽操作，按Delete可删除当前选中的对象
* 4.编辑好准备打印的内容后到“打印”TAB页，“保存配置”会将当前内容保存为XML文件
* 5.保存配置后可以“打印预览”，也可以直接“打印”
* 6.“读取配置”用于直接读取之前设计好的模板打印样式，文件保存在程序根目录中，默认模板为KopSoft.KopSoftPrint.PrintConfig.xml


##BS 客户端代码  >= .Net4.5

#安装Nuget Fleck    
```
using Fleck;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace WebSocketPrint
{
    class Program
    {
        static void Main(string[] args)
        {
            var allSockets = new List<IWebSocketConnection>();
            var server = new WebSocketServer("ws://192.168.206.163:50000");
            server.Start(socket =>
            {
                socket.OnOpen = () =>
                {
                    Console.WriteLine("Open!");
                    allSockets.Add(socket);
                };
                socket.OnClose = () =>
                {
                    Console.WriteLine("Close!");
                    allSockets.Remove(socket);
                };
                socket.OnMessage = message =>
                {
                   //此处可处理打印逻辑
                    Console.WriteLine(message);
                    allSockets.ToList().ForEach(s => s.Send("Echo: " + message));
                };
            });


            var input = Console.ReadLine();
            while (input != "exit")
            {
                foreach (var socket in allSockets.ToList())
                {
                    socket.Send(input);
                }
                input = Console.ReadLine();
            }

        }
    }
}

```








