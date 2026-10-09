import React, { useState, useEffect } from 'react';
import { 
  Dog, Calendar, CheckSquare, AlertTriangle, CreditCard, 
  CheckCircle, Clock, ShieldCheck, Activity, Users, 
  ChevronRight, ArrowLeft, Home, Scissors, UserCheck
} from 'lucide-react';

export default function App() {
  // --- Global State ---
  // 'home', 'booking', 'day-of-service', 'admin'
  const [currentView, setCurrentView] = useState('home'); 
  
  // --- Booking State ---
  const [bookingStep, setBookingStep] = useState(1);
  const [bookingData, setBookingData] = useState({
    petName: '',
    breed: '小型犬',
    ownerName: '',
    trimmer: '',
    date: '',
    time: '',
    agreedToStay: false
  });

  // --- Day of Service State ---
  // 'waiting' (開始前), 'in-progress' (施術中), 'completed' (終了)
  const [dayStatus, setDayStatus] = useState('waiting');
  const [userStarted, setUserStarted] = useState(false);
  const [trimmerStarted, setTrimmerStarted] = useState(false);
  const [userEnded, setUserEnded] = useState(false);
  const [trimmerEnded, setTrimmerEnded] = useState(false);

  // --- Admin Logs State ---
  const [logs, setLogs] = useState([
    { time: new Date().toLocaleTimeString(), type: 'SYSTEM', msg: 'システム起動完了' }
  ]);

  // Helper to add logs
  const addLog = (msg, type = 'LOG') => {
    setLogs(prev => [{ time: new Date().toLocaleTimeString(), type, msg }, ...prev]);
  };

  // Watch for mutual button presses to change day status
  useEffect(() => {
    if (dayStatus === 'waiting' && userStarted && trimmerStarted) {
      setDayStatus('in-progress');
      addLog('相互「利用開始」確認完了 ➔ ステータス【施術中】へ更新', 'SUCCESS');
    }
    if (dayStatus === 'in-progress' && userEnded && trimmerEnded) {
      setDayStatus('completed');
      addLog('相互「終了」確認完了 ➔ ブース解放', 'SUCCESS');
    }
  }, [userStarted, trimmerStarted, userEnded, trimmerEnded, dayStatus]);

  const HomeView = () => (
    <div className="max-w-2xl mx-auto p-6 text-center">
      <div className="mb-8">
        <Dog className="w-16 h-16 mx-auto text-amber-600 mb-4" />
        <h1 className="text-3xl font-bold text-gray-800">K・DogSpa 予約システム</h1>
        <p className="text-gray-500 mt-2">（プロトタイプ版）</p>
      </div>
      
      <div className="grid gap-4 md:grid-cols-3">
        <button 
          onClick={() => { setCurrentView('booking'); setBookingStep(1); }}
          className="p-6 bg-white border-2 border-amber-200 rounded-xl hover:bg-amber-50 transition shadow-sm flex flex-col items-center"
        >
          <Calendar className="w-8 h-8 text-amber-500 mb-3" />
          <span className="font-bold text-gray-800">予約フェーズ</span>
          <span className="text-xs text-gray-500 mt-2">お客様の予約フローを体験</span>
        </button>

        <button 
          onClick={() => setCurrentView('day-of-service')}
          className="p-6 bg-white border-2 border-teal-200 rounded-xl hover:bg-teal-50 transition shadow-sm flex flex-col items-center"
        >
          <UserCheck className="w-8 h-8 text-teal-500 mb-3" />
          <span className="font-bold text-gray-800">当日マイページ</span>
          <span className="text-xs text-gray-500 mt-2">同席確認・ステータス更新</span>
        </button>

        <button 
          onClick={() => setCurrentView('admin')}
          className="p-6 bg-white border-2 border-gray-200 rounded-xl hover:bg-gray-50 transition shadow-sm flex flex-col items-center"
        >
          <Activity className="w-8 h-8 text-gray-600 mb-3" />
          <span className="font-bold text-gray-800">管理者画面</span>
          <span className="text-xs text-gray-500 mt-2">リアルタイム稼働・ログ監視</span>
        </button>
      </div>
    </div>
  );

  const BookingView = () => {
    
    const handleNext = () => setBookingStep(prev => prev + 1);
    const handlePrev = () => setBookingStep(prev => prev - 1);

    const StepIndicator = () => (
      <div className="flex items-center justify-center space-x-2 mb-8 text-sm">
        {[1, 2, 3, 4, 5].map((step) => (
          <React.Fragment key={step}>
            <div className={`flex items-center justify-center w-8 h-8 rounded-full font-bold ${
              bookingStep === step ? 'bg-amber-500 text-white' : 
              bookingStep > step ? 'bg-amber-200 text-amber-800' : 'bg-gray-200 text-gray-500'
            }`}>
              {step}
            </div>
            {step < 5 && <div className={`w-8 h-1 rounded ${bookingStep > step ? 'bg-amber-200' : 'bg-gray-200'}`} />}
          </React.Fragment>
        ))}
      </div>
    );

    const Step1 = () => (
      <div className="space-y-6 animate-in fade-in slide-in-from-bottom-4 duration-500">
        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <h2 className="text-xl font-bold mb-4 border-b pb-2 flex items-center">
            <Dog className="mr-2 text-amber-500" /> コース概要
          </h2>
          <div className="bg-amber-50 p-4 rounded-lg">
            <p className="font-bold text-amber-900">トリマーお任せコース（要お付き添い）</p>
            <p className="text-sm text-amber-800 mt-1">爪切り、耳掃除、肛門腺絞り、足裏カット、低刺激シャンプー、保湿トリートメント</p>
            <div className="mt-2 flex gap-4 text-sm font-semibold text-amber-900">
              <span>目安: 60分</span>
              <span>料金: 6,500円（税込）</span>
            </div>
          </div>
        </div>

        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100 space-y-4">
          <h2 className="text-xl font-bold mb-2">愛犬・飼い主情報</h2>
          <div>
            <label className="block text-sm font-bold text-gray-700 mb-1">愛犬のお名前</label>
            <input 
              type="text" 
              className="w-full p-2 border rounded-md"
              value={bookingData.petName}
              onChange={(e) => setBookingData({...bookingData, petName: e.target.value})}
              placeholder="例：ポチ"
            />
          </div>
          <div>
            <label className="block text-sm font-bold text-gray-700 mb-1">飼い主様 氏名</label>
            <input 
              type="text" 
              className="w-full p-2 border rounded-md"
              value={bookingData.ownerName}
              onChange={(e) => setBookingData({...bookingData, ownerName: e.target.value})}
              placeholder="例：山田 太郎"
            />
          </div>
        </div>
        
        <div className="flex justify-end">
          <button onClick={handleNext} disabled={!bookingData.petName || !bookingData.ownerName} 
            className="bg-amber-500 text-white px-6 py-3 rounded-lg font-bold hover:bg-amber-600 disabled:opacity-50 flex items-center">
            日時・指名へ進む <ChevronRight className="w-5 h-5 ml-1" />
          </button>
        </div>
      </div>
    );

    const Step2 = () => (
      <div className="space-y-6 animate-in fade-in slide-in-from-bottom-4 duration-500">
        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <h2 className="text-xl font-bold mb-4">担当トリマー指名</h2>
          <div className="grid grid-cols-2 gap-4">
            {['指名なし', '佐藤トリマー', '鈴木トリマー'].map(name => (
              <label key={name} className={`border p-4 rounded-lg cursor-pointer flex items-center space-x-3 ${bookingData.trimmer === name ? 'border-amber-500 bg-amber-50' : 'hover:bg-gray-50'}`}>
                <input type="radio" name="trimmer" value={name} 
                  checked={bookingData.trimmer === name}
                  onChange={(e) => setBookingData({...bookingData, trimmer: e.target.value})}
                  className="w-5 h-5 text-amber-500 focus:ring-amber-500" 
                />
                <span className="font-bold text-gray-700">{name}</span>
              </label>
            ))}
          </div>
        </div>

        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <h2 className="text-xl font-bold mb-4">日時選択</h2>
          <input 
            type="date" 
            className="w-full p-3 border rounded-lg mb-4"
            value={bookingData.date}
            onChange={(e) => setBookingData({...bookingData, date: e.target.value})}
          />
          <div className="grid grid-cols-3 gap-3">
            {['10:00', '11:30', '13:00', '14:30', '16:00'].map(time => (
              <button key={time} 
                onClick={() => setBookingData({...bookingData, time})}
                className={`py-2 rounded-md font-bold border ${bookingData.time === time ? 'bg-amber-500 text-white border-amber-500' : 'text-gray-600 border-gray-200 hover:bg-gray-50'}`}>
                {time}
              </button>
            ))}
          </div>
        </div>

        <div className="flex justify-between">
          <button onClick={handlePrev} className="text-gray-500 px-4 py-2 font-bold flex items-center hover:bg-gray-100 rounded-lg">
            <ArrowLeft className="w-5 h-5 mr-1" /> 戻る
          </button>
          <button onClick={handleNext} disabled={!bookingData.trimmer || !bookingData.date || !bookingData.time} 
            className="bg-amber-500 text-white px-6 py-3 rounded-lg font-bold hover:bg-amber-600 disabled:opacity-50 flex items-center">
            同席確認同意へ進む <ChevronRight className="w-5 h-5 ml-1" />
          </button>
        </div>
      </div>
    );

    const Step3 = () => (
      <div className="space-y-6 animate-in fade-in slide-in-from-bottom-4 duration-500">
        <div className="bg-red-50 border-2 border-red-500 p-6 rounded-xl shadow-sm">
          <h2 className="text-2xl font-bold text-red-700 mb-4 flex items-center">
            <AlertTriangle className="w-8 h-8 mr-2" /> 【重要】ブース内常時同席について
          </h2>
          <div className="text-red-900 space-y-3 leading-relaxed mb-6 bg-white p-4 rounded-lg bg-opacity-60">
            <p>本コースはワンちゃんの安全確保とリラックスした施術のため、飼い主様がブース内に常時お立ち会いいただくことが利用条件となっております。</p>
            <p className="font-bold border-b border-red-300 pb-2">開始から終了までの約60分間、ブース内でお付き添いをお願いいたします。</p>
            <p className="text-sm">※お付き添いいただけない場合は、施術をお断りさせていただく場合がございます。</p>
          </div>
          
          <label className="flex items-start space-x-3 cursor-pointer bg-white p-4 rounded-lg border-2 border-red-200 hover:border-red-400 transition">
            <input 
              type="checkbox" 
              checked={bookingData.agreedToStay}
              onChange={(e) => setBookingData({...bookingData, agreedToStay: e.target.checked})}
              className="w-6 h-6 text-red-600 rounded border-gray-300 focus:ring-red-500 mt-1"
            />
            <span className="font-bold text-lg text-red-800">
              施術中、ブース内で常時同席することに同意します
            </span>
          </label>
        </div>

        <div className="flex justify-between">
          <button onClick={handlePrev} className="text-gray-500 px-4 py-2 font-bold flex items-center hover:bg-gray-100 rounded-lg">
            <ArrowLeft className="w-5 h-5 mr-1" /> 戻る
          </button>
          <button onClick={handleNext} disabled={!bookingData.agreedToStay} 
            className="bg-amber-500 text-white px-6 py-3 rounded-lg font-bold hover:bg-amber-600 disabled:opacity-50 flex items-center transition-opacity">
            確認・決済画面へ進む <ChevronRight className="w-5 h-5 ml-1" />
          </button>
        </div>
      </div>
    );

    const Step4 = () => (
      <div className="space-y-6 animate-in fade-in slide-in-from-bottom-4 duration-500">
        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <h2 className="text-xl font-bold mb-4 border-b pb-2">予約内容の確認</h2>
          <ul className="space-y-3 text-gray-700">
            <li className="flex justify-between"><span>コース:</span> <span className="font-bold">トリマーお任せコース</span></li>
            <li className="flex justify-between"><span>日時:</span> <span className="font-bold">{bookingData.date} {bookingData.time}〜</span></li>
            <li className="flex justify-between"><span>担当:</span> <span className="font-bold">{bookingData.trimmer}</span></li>
            <li className="flex justify-between"><span>愛犬:</span> <span className="font-bold">{bookingData.petName}</span></li>
            <li className="flex justify-between border-t pt-3 mt-3 text-red-600">
              <span>同席同意:</span> <span className="font-bold flex items-center"><CheckCircle className="w-4 h-4 mr-1"/> 同意済み（常時同席）</span>
            </li>
          </ul>
        </div>

        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <h2 className="text-xl font-bold mb-4 flex items-center"><CreditCard className="w-5 h-5 mr-2 text-gray-500"/> クレジットカード決済</h2>
          <div className="space-y-4">
            <input type="text" placeholder="カード番号 (ダミー)" className="w-full p-3 border rounded-lg bg-gray-50" />
            <div className="grid grid-cols-2 gap-4">
              <input type="text" placeholder="MM/YY" className="w-full p-3 border rounded-lg bg-gray-50" />
              <input type="text" placeholder="CVC" className="w-full p-3 border rounded-lg bg-gray-50" />
            </div>
          </div>
        </div>

        <div className="flex justify-between">
          <button onClick={handlePrev} className="text-gray-500 px-4 py-2 font-bold flex items-center hover:bg-gray-100 rounded-lg">
            <ArrowLeft className="w-5 h-5 mr-1" /> 戻る
          </button>
          <button onClick={() => {
              handleNext();
              addLog(`予約完了 - 愛犬:${bookingData.petName} (決済完了 6,500円)`, 'SUCCESS');
              addLog(`[AUTO_MAIL] 予約確定メール送信 ➔ ${bookingData.ownerName}様`, 'SYSTEM');
            }} 
            className="bg-green-600 text-white px-6 py-3 rounded-lg font-bold hover:bg-green-700 shadow-md">
            予約を確定して決済する（6,500円）
          </button>
        </div>
      </div>
    );

    const Step5 = () => (
      <div className="text-center space-y-6 animate-in zoom-in duration-500 py-8">
        <CheckCircle className="w-20 h-20 text-green-500 mx-auto" />
        <h2 className="text-3xl font-bold text-gray-800">予約が完了しました</h2>
        <p className="text-gray-500 text-lg">予約ID: #KD-{Math.floor(Math.random() * 90000) + 10000}</p>
        
        <div className="bg-amber-50 text-left p-6 rounded-xl border border-amber-200 mt-8">
          <h3 className="font-bold text-amber-900 mb-2">当日のご案内</h3>
          <ul className="list-disc pl-5 space-y-2 text-amber-800 text-sm">
            <li>予約開始10分前に、ご登録のメールアドレスへ『同席確認メール』をお送りします。</li>
            <li>メール内のURLよりマイページにログインし、トリマーと一緒に『利用開始』ボタンを押してください。</li>
          </ul>
        </div>

        <div className="flex justify-center space-x-4 mt-8">
          <button onClick={() => setCurrentView('home')} className="px-6 py-3 border border-gray-300 text-gray-700 rounded-lg font-bold hover:bg-gray-50">
            トップへ戻る
          </button>
          <button onClick={() => setCurrentView('day-of-service')} className="px-6 py-3 bg-teal-600 text-white rounded-lg font-bold hover:bg-teal-700 shadow-md">
            当日マイページを体験 ➔
          </button>
        </div>
      </div>
    );

    return (
      <div className="max-w-3xl mx-auto p-4 md:p-8">
        <div className="flex justify-between items-center mb-8">
          <h1 className="text-2xl font-bold text-gray-800">ご予約</h1>
          <button onClick={() => setCurrentView('home')} className="p-2 text-gray-400 hover:bg-gray-100 rounded-full">
            <Home className="w-6 h-6" />
          </button>
        </div>
        
        {bookingStep < 5 && <StepIndicator />}
        
        {bookingStep === 1 && <Step1 />}
        {bookingStep === 2 && <Step2 />}
        {bookingStep === 3 && <Step3 />}
        {bookingStep === 4 && <Step4 />}
        {bookingStep === 5 && <Step5 />}
      </div>
    );
  };

  const DayOfServiceView = () => {
    
    // Simulating sending the auto mail 10 mins before
    const simulate10MinMail = () => {
      addLog(`[AUTO_MAIL] 開始10分前 同席確認メール送信 ➔ ユーザー・トリマー`, 'SYSTEM');
      alert("システムログ: 「開始10分前メール」が送信されました。");
    };

    return (
      <div className="max-w-4xl mx-auto p-4 md:p-8">
        <div className="flex justify-between items-center mb-8">
          <h1 className="text-2xl font-bold text-gray-800">当日マイページ (シミュレーション)</h1>
          <button onClick={() => setCurrentView('home')} className="p-2 text-gray-400 hover:bg-gray-100 rounded-full">
            <Home className="w-6 h-6" />
          </button>
        </div>

        {/* Status Banner */}
        <div className={`p-4 rounded-xl mb-8 text-center font-bold text-xl shadow-sm ${
          dayStatus === 'waiting' ? 'bg-amber-100 text-amber-800 border-2 border-amber-300' :
          dayStatus === 'in-progress' ? 'bg-blue-100 text-blue-800 border-2 border-blue-300' :
          'bg-gray-100 text-gray-800 border-2 border-gray-300'
        }`}>
          {dayStatus === 'waiting' && '【開始前】同席確認待ち'}
          {dayStatus === 'in-progress' && '【施術中】ブース内同席中'}
          {dayStatus === 'completed' && '【施術完了】お疲れ様でした'}
        </div>

        <div className="grid md:grid-cols-2 gap-8">
          {/* USER SIDE UI */}
          <div className="border border-gray-200 rounded-xl overflow-hidden shadow-sm">
            <div className="bg-teal-600 text-white p-3 font-bold text-center">飼い主様 画面</div>
            <div className="p-6 bg-white min-h-[300px] flex flex-col items-center justify-center">
              {dayStatus === 'waiting' && (
                <>
                  <p className="text-sm text-gray-500 mb-6 text-center">トリマーと一緒に、開始ボタンを押してください。</p>
                  <button 
                    onClick={() => {
                      setUserStarted(true);
                      addLog(`ユーザー「利用開始」ボタン押下`, 'ACTION');
                    }}
                    disabled={userStarted}
                    className={`w-full py-4 rounded-xl font-bold text-lg shadow-md transition ${userStarted ? 'bg-gray-300 text-gray-500' : 'bg-teal-500 text-white hover:bg-teal-600 hover:scale-105'}`}
                  >
                    {userStarted ? '確認済み (トリマー待ち)' : '同席確認・利用開始'}
                  </button>
                </>
              )}

              {dayStatus === 'in-progress' && (
                <div className="w-full space-y-4">
                  <div className="text-center p-4 bg-gray-50 rounded-lg border">
                    <p className="text-xs text-gray-500 font-bold mb-1">残り時間目安</p>
                    <p className="text-4xl font-mono text-gray-800">59:58</p>
                  </div>
                  <button 
                    onClick={() => {
                      setUserEnded(true);
                      addLog(`ユーザー「終了確認」ボタン押下`, 'ACTION');
                    }}
                    disabled={userEnded}
                    className={`w-full py-3 rounded-xl font-bold shadow-md transition mt-8 ${userEnded ? 'bg-gray-300 text-gray-500' : 'bg-gray-800 text-white hover:bg-gray-900'}`}
                  >
                    {userEnded ? '確認済み' : '終了確認 (ブース退出)'}
                  </button>
                </div>
              )}

              {dayStatus === 'completed' && (
                <div className="text-center">
                  <CheckCircle className="w-16 h-16 text-gray-400 mx-auto mb-4" />
                  <p className="text-gray-600 font-bold">ご利用ありがとうございました</p>
                </div>
              )}
            </div>
          </div>

          {/* TRIMMER SIDE UI */}
          <div className="border border-gray-200 rounded-xl overflow-hidden shadow-sm">
            <div className="bg-indigo-600 text-white p-3 font-bold text-center">トリマー 画面</div>
            <div className="p-6 bg-white min-h-[300px] flex flex-col items-center justify-center">
               {dayStatus === 'waiting' && (
                <>
                  <p className="text-sm text-gray-500 mb-6 text-center">飼い主様が同席していることを確認し、開始してください。</p>
                  <button 
                    onClick={() => {
                      setTrimmerStarted(true);
                      addLog(`トリマー「利用開始」ボタン押下`, 'ACTION');
                    }}
                    disabled={trimmerStarted}
                    className={`w-full py-4 rounded-xl font-bold text-lg shadow-md transition ${trimmerStarted ? 'bg-gray-300 text-gray-500' : 'bg-indigo-500 text-white hover:bg-indigo-600 hover:scale-105'}`}
                  >
                    {trimmerStarted ? '確認済み (ユーザー待ち)' : '同席確認・利用開始'}
                  </button>
                </>
              )}

              {dayStatus === 'in-progress' && (
                <div className="w-full space-y-3">
                  <div className="p-3 bg-indigo-50 rounded-lg text-sm font-bold text-indigo-900 border border-indigo-100">
                    <CheckSquare className="inline w-4 h-4 mr-1" /> 爪切り・耳掃除 完了
                  </div>
                  <div className="p-3 bg-gray-50 rounded-lg text-sm text-gray-500 border">
                    <div className="w-4 h-4 border-2 border-gray-300 rounded inline-block mr-2 align-middle"></div> 
                    シャンプー・トリートメント
                  </div>
                  
                  <button 
                    onClick={() => {
                      setTrimmerEnded(true);
                      addLog(`トリマー「終了確認」ボタン押下`, 'ACTION');
                    }}
                    disabled={trimmerEnded}
                    className={`w-full py-3 rounded-xl font-bold shadow-md transition mt-6 ${trimmerEnded ? 'bg-gray-300 text-gray-500' : 'bg-indigo-600 text-white hover:bg-indigo-700'}`}
                  >
                    {trimmerEnded ? '確認済み' : '施術完了・退出確認'}
                  </button>
                </div>
              )}

              {dayStatus === 'completed' && (
                <div className="text-center">
                  <Scissors className="w-16 h-16 text-gray-400 mx-auto mb-4" />
                  <p className="text-gray-600 font-bold">ブース解放完了</p>
                </div>
              )}
            </div>
          </div>
        </div>

        {/* Developer / Simulation Controls */}
        <div className="mt-8 border-t pt-8 text-center">
          <p className="text-xs text-gray-400 mb-2">※シミュレーション操作用</p>
          <div className="flex justify-center gap-4">
            <button onClick={simulate10MinMail} className="text-xs bg-gray-200 px-3 py-1 rounded hover:bg-gray-300 text-gray-700">
              [Sim] 10分前メール送信
            </button>
            <button onClick={() => {
              setDayStatus('waiting'); setUserStarted(false); setTrimmerStarted(false); setUserEnded(false); setTrimmerEnded(false);
              addLog('状態をリセットしました', 'SYSTEM');
            }} className="text-xs bg-red-100 px-3 py-1 rounded hover:bg-red-200 text-red-700">
              状態リセット
            </button>
          </div>
        </div>
      </div>
    );
  };

  const AdminView = () => (
    <div className="max-w-5xl mx-auto p-4 md:p-8 bg-gray-50 min-h-screen">
       <div className="flex justify-between items-center mb-8">
        <div>
          <h1 className="text-2xl font-bold text-gray-800 flex items-center">
            <ShieldCheck className="w-6 h-6 mr-2 text-indigo-600" /> 管理者ダッシュボード
          </h1>
          <p className="text-sm text-gray-500 mt-1">リアルタイム稼働状況監視・動作通知フィード</p>
        </div>
        <button onClick={() => setCurrentView('home')} className="p-2 bg-white border shadow-sm text-gray-600 hover:bg-gray-100 rounded-lg flex items-center">
          <Home className="w-4 h-4 mr-2" /> 戻る
        </button>
      </div>

      <div className="grid md:grid-cols-3 gap-6 mb-8">
        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100 flex items-center">
          <div className="p-4 bg-blue-100 rounded-full mr-4 text-blue-600"><Activity className="w-8 h-8" /></div>
          <div>
            <p className="text-sm text-gray-500 font-bold">現在施術中</p>
            <p className="text-3xl font-bold text-gray-800">{dayStatus === 'in-progress' ? '1' : '0'} <span className="text-lg font-normal">件</span></p>
          </div>
        </div>
        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100 flex items-center">
          <div className="p-4 bg-green-100 rounded-full mr-4 text-green-600"><CheckCircle className="w-8 h-8" /></div>
          <div>
            <p className="text-sm text-gray-500 font-bold">本日予約総数</p>
            <p className="text-3xl font-bold text-gray-800">12 <span className="text-lg font-normal">件</span></p>
          </div>
        </div>
        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100 flex items-center">
          <div className="p-4 bg-purple-100 rounded-full mr-4 text-purple-600"><Users className="w-8 h-8" /></div>
          <div>
            <p className="text-sm text-gray-500 font-bold">ブース稼働率</p>
            <p className="text-3xl font-bold text-gray-800">75 <span className="text-lg font-normal">%</span></p>
          </div>
        </div>
      </div>

      <div className="bg-white rounded-xl shadow-sm border border-gray-100 overflow-hidden">
        <div className="bg-gray-800 text-white p-4 font-bold flex justify-between items-center">
          <span>リアルタイムログ (System Feed)</span>
          <span className="flex items-center text-xs text-green-400">
            <span className="w-2 h-2 bg-green-400 rounded-full mr-2 animate-pulse"></span> Live
          </span>
        </div>
        <div className="h-[400px] overflow-y-auto p-4 space-y-2 bg-black font-mono text-sm">
          {logs.map((log, i) => (
            <div key={i} className="border-b border-gray-800 pb-2">
              <span className="text-gray-500">[{log.time}]</span>{' '}
              <span className={`
                ${log.type === 'SUCCESS' ? 'text-green-400' : ''}
                ${log.type === 'SYSTEM' ? 'text-blue-400' : ''}
                ${log.type === 'ACTION' ? 'text-amber-400' : ''}
                ${log.type === 'LOG' ? 'text-gray-300' : ''}
              `}>
                [{log.type}]
              </span>{' '}
              <span className="text-gray-200">{log.msg}</span>
            </div>
          ))}
        </div>
      </div>
    </div>
  );

  return (
    <div className="min-h-screen bg-gray-50 font-sans text-gray-900 pb-12">
      {currentView === 'home' && <HomeView />}
      {currentView === 'booking' && <BookingView />}
      {currentView === 'day-of-service' && <DayOfServiceView />}
      {currentView === 'admin' && <AdminView />}
    </div>
  );
}
