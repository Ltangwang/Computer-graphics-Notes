

```cpp
for (auto& light : lights)
    {
        // TODO: For each light source in the code, calculate what the *ambient*, *diffuse*, and *specular* 
        // components are. Then, accumulate that result on the *result_color* object.
        // components are. Then, accumulate that result on the *result_color* object.
        Eigen::Vector3f I=light.intensity;            //定义一个光的强度
        Eigen::Vector3f P=(light.position-point).normalized();   //定义光和一个点的距离并且标准化
        Eigen::Vector3f N=normal.normalized();                   //法向量标准化
        Eigen::Vector3f V=(eye_pos-point).normalized();          //定义了相机到点的距离并且标准化
        Eigen::Vector3f H=(P+V).normalized();                    //半角向量H的标准化

        float R=(light.position-point).dot((light.position-point));


        Eigen::Vector3f La=ka.cwiseProduct(amb_light_intensity);          //计算LA
        Eigen::Vector3f Ld=kd.cwiseProduct(I/R)*std::max(0.f,N.dot(P));   //计算Ld
        Eigen::Vector3f Ls=ks.cwiseProduct(I/R)*std::pow (std::max(0.f,N.dot(H)),p);   //计算LS
        result_color=result_color+La+Ld+Ls;                                 //计算总的颜色

    }
```