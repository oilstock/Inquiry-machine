   if($kj_num > 0){
                $data = M('product') -> find($kj_id);
                if(!empty($data)){
                    for($i=1;$i<=$kj_num;$i++){
                        $map = array();
                        $yCode = array('A', 'B', 'C', 'D', 'E', 'F', 'Q', 'Q', 'I', 'J');
                        $map['kjbh'] = $yCode[intval(date('Y')) - 2011] . date('d') . substr(time(), -5) . sprintf('%02d', rand(0, 99));
                        $map['user'] = session('username');
                        $map['user_id'] = $shequn['member'];
                        $map['project']= $data['title'];
                        $map['sid'] = $data['id'];
                        $map['yxzq'] = $data['yszq'];
                        $map['sumprice'] = $data['price'];
                        $map['addtime'] = date('Y-m-d H:i:s');
                        $map['imagepath'] = $data['thumb'];
                        $map['lixi']	= $data['gonglv'];
                        $map['kjsl'] =  $data['shouyi'];
                        $map['zt'] =  1;
                        $map['UG_getTime'] =  time();
                        M('order')->add($map);
                        jinbi($shequn['member'],0,'Community award'.$data['title'],1,5);
                        M('product')->where(array("id"=>$kj_id))->setDec("stock");
                    }
                }
            }
