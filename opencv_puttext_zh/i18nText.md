先安装freetype，然后编译lib18nText.so
编译主程序时加上
-I/usr/include/freetype2 -L/usr/local/lib/ -lfreetype -L./ -li18nText

#include "i18nText.h"

i18nText i18n;

// Convert const char* to const wchar_t*.
const wchar_t *GetWC(const char *c)
{
	setlocale(LC_CTYPE, "C.UTF-8");  
	const size_t cSize = strlen(c)+1;
	wchar_t* wc = new wchar_t[cSize];
	mbstowcs (wc, c, cSize);

	return wc;
}

init()
{
	...
	if (i18n.setFont("./MSYH.TTC")) { //字体
		SizeDesc fontSize; 
		fontSize.pixelSize = 30; fontSize.space = 0.5; fontSize.gap = 0.1;
		i18n.setSize(&fontSize);
	}
	...
}

main()
{
	...
	string strTemp = "中文示例";
	const wchar_t *msg = GetWC(strTemp.c_str());
	i18n.putText(image, msg, cv::Point(30, 40), cv::Scalar(255,255,255));
	...
}
