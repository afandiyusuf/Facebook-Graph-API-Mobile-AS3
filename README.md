# Facebook-Graph-API-Mobile-AS3
Facebook graph api as3 v2.2

# Example Script

package  {
	
	import flash.display.MovieClip;
	import com.facebook.graph.FacebookMobile;
	import flash.media.StageWebView;
	import flash.geom.Rectangle;
	import com.facebook.graph.core.FacebookURLDefaults;
	
	public class Main extends MovieClip {
		private var swv:StageWebView = new StageWebView();
		
		public function Main() {
			FacebookMobile.init("you_app_id",callbackInit); //you can create at developers.facebook.com
			FacebookURLDefaults.LOGIN_SUCCESS_URL = "your_url_callback" //must be same with your facebook app url
			var rect:Rectangle = new Rectangle(0,0,stage.stageWidth,stage.stageHeight);
			
			swv.stage = this.stage;
			swv.viewPort = rect;
			
		}
		private function callbackInit(success:*,error:*)
		{
			var arr:Array = new Array("user_photos","user_publish"); //you must submit review to facebook for extended permission like (user_photos,user_publish,etc)
			
			trace(success,error);
			FacebookMobile.login(LoginSuccess,stage,arr,swv);
		}
		private function LoginSuccess(success:*,error:*)
		{
			trace(success,error);
			
			FacebookMobile.api("/me",succesMe);
		}
		private function succesMe(success:*,error:*)
		{
			trace(success,error);
			
			//USE THIS FOR LOG OUT AND CLEAR CACHE
			FacebookMobile.logout(LogoutSuccess);
		}
		private function LogoutSuccess(response:*)
		{
			trace("logout",response);
		}
	}
}
