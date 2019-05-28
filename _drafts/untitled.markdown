---
layout: post
title: "(Untitled)"
---

Googles ARCore sdk for augmented reality

Entry point for SDK CBCameraActivity (IntentUtils launchCameraIntent used in MatchActivity)

SynAdapter we are calling Rest API call to fetch the colors and inserting it in to Database

Camera (capturing pics, loading images, reducing image size) functionality we are handling in Cambrian sdk.

ColorUtils we have it in app level.

Live View invokes CBVideoPainter class

Room (ORM)


interfaces for model and presenter
Make networking classes as a library


package com.demo.weatherforecast.data.webservices;

import android.graphics.Bitmap;
import android.net.Uri;
import android.os.Bundle;
import android.support.annotation.NonNull;
import android.util.Log;
import android.widget.ImageView;

import com.android.volley.Request;
import com.android.volley.Response;
import com.android.volley.VolleyError;
import com.android.volley.toolbox.ImageRequest;
import com.demo.weatherforecast.app.AppController;
import com.demo.weatherforecast.data.webservices.volley.requests.GetRequest;
import com.demo.weatherforecast.model.WeatherData;
import com.demo.weatherforecast.util.Constants;
import com.demo.weatherforecast.util.ErrorHandler;
import com.google.gson.Gson;

/**
 * Created by ramya on 10/9/17.
 */

public class WebApiUtil {

    private static WebApiUtil sInstance;
    private static final String TAG = WebApiUtil.class.getSimpleName();

    /**
     * Factory method to get web util instance
     *
     * @return {@link WebApiUtil} object
     */
    @NonNull
    public static WebApiUtil getInstance() {

        if (sInstance == null) {
            sInstance = new WebApiUtil();
        }
        return sInstance;
    }


    public void sendWeatherForecastListener(String requestType, Bundle params, final WebServiceResponseInterface callback, String tag){
        GetRequest getRequest;
        Uri uri = null;
        int methodType = Request.Method.GET;
        if(requestType.equals(Constants.OPEN_WEATHER_API)){
            String city = params.getString(Constants.CITY);
            uri  = Uri.parse(Constants.OPEN_WEATHER_API).buildUpon()
                    .appendQueryParameter(Constants.WEATHER_FORECAST_PARAM, city)
                    .appendQueryParameter(Constants.UNITS_PARAM, Constants.METRICS_PARAM)
                    .appendQueryParameter(Constants.APP_ID_PARAM, Constants.APP_ID)
                    .build();
        }
        getRequest = new GetRequest(methodType, uri.toString(), getWeatherForecastSuccessListener(requestType, callback),
                getWebserviceErrorListener(callback));
        getRequest.setShouldCache(false);
        AppController.getInstance().addToRequestQueue(getRequest, tag);
    }

    //SuccessListener
    private static Response.Listener<String> getWeatherForecastSuccessListener(final String requestType, final WebServiceResponseInterface callback) {
        return new Response.Listener<String>() {
            @Override
            public void onResponse(String response) {
                try {
                    if (requestType.equals(Constants.OPEN_WEATHER_API)) {
                        WeatherData weatherData = new Gson().fromJson(response, WeatherData.class);
                        callback.onSuccess(weatherData);
                    }
                } catch (Exception e) {
                    Log.d(TAG, e.getMessage(), e);
                }
            }
        };
    }

    public void sendWeatherForecastImageListener(String requestType, Bundle params, final WebServiceImageResponseInterface callback, String tag){
        ImageRequest imageRequest;
        Uri uri = null;
        if(requestType.equals(Constants.OPEN_WEATHER_IMAGE_API)){
            String imageId = params.getString(Constants.IMAGE_ID);
            uri  = Uri.parse(Constants.OPEN_WEATHER_IMAGE_API).buildUpon()
                    .appendPath(imageId + Constants.PNG_EXTENSION)
                    .build();
        }
        imageRequest = new ImageRequest(uri.toString(), getWeatherForecastImageSuccessListener(requestType, callback),300, 200, ImageView.ScaleType.FIT_XY, Bitmap.Config.ARGB_8888,
                getWebserviceImageErrorListener(callback));
        imageRequest.setShouldCache(false);
        AppController.getInstance().addToRequestQueue(imageRequest, tag);
    }

    //SuccessListener
    private static Response.Listener<Bitmap> getWeatherForecastImageSuccessListener(final String requestType, final WebServiceImageResponseInterface callback) {
        return new Response.Listener<Bitmap>() {
            @Override
            public void onResponse(Bitmap response) {
                try {
                    if (requestType.equals(Constants.OPEN_WEATHER_IMAGE_API)) {
                            callback.onSuccess(response);
                    }
                } catch (Exception e) {
                    Log.d(TAG, e.getMessage(), e);
                }
            }
        };
    }

    //Error Listener
    private static Response.ErrorListener getWebserviceErrorListener(final WebServiceResponseInterface callback) {
        return new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                callback.onError(ErrorHandler.getInternalErrorCode(error), error.getMessage());
            }
        };
    }

    //Error Listener
    private static Response.ErrorListener getWebserviceImageErrorListener(final WebServiceImageResponseInterface callback) {
        return new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                callback.onError(ErrorHandler.getInternalErrorCode(error), error.getMessage());
            }
        };
    }
}



Camera -----> show camera(in app)
store image in gallery
permission management

loading image @camera or disk

color selection  ----> Given a frame/image
use palette API to get color sw

color code for paintbrand
migrate existing DB
DAO to offer search methods

rx libraries for permissions
android annotation vs butterknife
