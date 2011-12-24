SparkleMotion is a python package for creating [Sparkle](http://sparkle.andymatuschak.org) updates.

To use it subclass `SparkleMotion`, set the required variables and overwrite any functions you want to format the various files and labels. 

``` python
class ChopShopUpdate(SparkleMotion):
    urlRoot = 'http://appcast.inscopeapps.com/ChopShop/'
    appPath = '/mercurial/projects/ChopShop/build/Release/ChopShop.app'
    privPemPath = '/mercurial/projects/ChopShop/Sparkle/dsa_priv.pem'
    stagingAreaPath = '/mercurial/projects/ChopShop/Sparkle/StagingArea'
    appCastFileName = 'AppCast.xml'
        
    def zipFileName(self):
        return '%s-%s.%s.zip' % (self.appName(), self.shortVersionString().split()[0], self.version())
        
    def releaseNotesFileName(self):
        return '%s.%s.html' % (self.shortVersionString().split()[0], self.version())
        
    def updateTitle(self):
        return 'Version %s - Build %s' % (self.shortVersionString().split('(')[0], self.version())
        
    def defaultNote(self):
        return '''
        <ul>
	       <li>
	           <h1>Sweet new feature</h1>
	           <span>This new feature is going to rock!</span>
	       </li>
	   </ul>
	   '''
        
ChopShopUpdate().run()
```